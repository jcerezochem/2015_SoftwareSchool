(this presesntation is in the git repo, in apple keynote format)

# BLAS
**************

* BLAS1
Involve vectors
  - vector norm
  - AXPY: 

* BLAS2
Matrix-vector operations
  - Product of matrix and vectors

* BLAS3
Matrix-matrix operations
  - Matrix products: GEMM

# LAPACK
**************
* Linear Algebra PACKage
so all algebra not covered by BLAS
  - Eigenvalues problems: there are high level programs for that
  - There are alos lower level alhorithms, such as QR decomposition, to split the problem

* Naming conventions
  - S = single precision
  - D double
  - C comlex
  - Z complex double

# Array allocation
**********************

Matrix are stored by columns in FORTRAN and by rows in C/C++. Note also that in FORTRAN all matrix elements are stored in contiguous positions of the memory. This is not necessarily the case in C/C++, there only within a row the elemnts are stored contiguously, when we change the row, the posibion might not be contiguous. BLAS and LAPACK, assume that the arrays are stored contiguously.

--------
## <font color='red'>NOTE</font>: About the language BLAS and LAPACK are written

It is thought that they are written in FORTRAN, but actually, underneath, there is more efficient machine implementation. Is the interface which is written in FORTRAN, so we need to call the FORTRAN interface if we want to use them in C/C++

-------

The fact that "FORTRAN is the transpose of C/C++", means that we need to take care about the order (we need to reverse the order of the input matrices)


# Implementations of BLAS/LAPACK
*********************************

* Netlib (free)
* Intel MKL ($$)
* IMB ESSL ($$)
* GotoBLAS (GPL)
* ATLAS (BSD)

ATLAS is good, and is a good alternative to MKL, which are the best ones


# Hands-on
**************
In Blueridge. Clone the repo: git remote add origin git clone https://github.com/lothian/S2I2.git

---------------------
### <font color='red'>NOTE</font>

In order to allocate memory contiguously in C/C++ (as is needed for BLAS/LAPACK), we need to add:

  `memset(static_cast<void*>(B), 0, row*col*sizeof(double));`

---------------------

# Matrix multimplication (see mm/mm.c code in the repo)
*********************************************************

## This are the results for a normal multimplication (any lib is used)

### Normal-Normal (the numbers are not right)
N     | time(s) 
------|-----------
100   | 0.01
500   | 0.84
800   | 3.45
1000  | 6.73
1200  | 11.63

We now tune the access to memory, so it is accessed contiguously.

### Normal transpose 
N     | time(s) 
------|-----------
100   | 0.01
500   | 0.84
800   | 3.45
1000  | 6.73
1200  | 11.63

## Using compiler flag: -O (basic optimization)
N     | time(s) 
------|-----------
100   | 0.00
500   | 0.43
800   | 1.78
1000  | 3.47
1200  | 6.01
2000  | 

## -O3
N     | time(s) 
------|-----------
100   | 0.00
500   | 0.15
800   | 0.62
1000  | 0.62
2000  | 11.3

Even better. But still will be worse than the libraries.

---------------------------------------------
### <font color='red'>NOTE</font>: calling gemm from C/C++

The arrays need to be passed as `double*`, i.e. an address, not the values of the array. 
This is because we need to pass it by adress not by value (as per BLAS documentation for BLAS).
So, we are passing the the address of the first element of the array:


| `A[0][0]` | `A[0][1]` |...| `A[0][N]` | `A[1][0]` |...|
|-----------|-----------|---|-----------|-----------|---|

The address of `A[0][0]` is stored in `A[0]`. I.e. `&A[0][0] = A[0]`

Furthermore, BLAS/LAPACK will expect that in the second positon would be A[1][0] instead of A[0][1], so 
we are actually using the transpose, and we are getting the transpose Product matrix. We have to take
this into account (although is not very difficult, only differnce may arrise in things like how eigenvectors
are stored, which are actually stored by row in C and by column in FORTRAN LAPACK)

---------------------------------------------

## Netlib LAPACK with no optimization when compiling them
N     | time(s) 
------|-----------
100   | 0.00
500   | 0.48
800   | 1.95
1000  | 3.79
1200  | 6.55
2000  | 31.69

----------------------
### <font color='red'>NOTE</font>

The BLAS libraries for C/C++ are called with the name followied by underscore, e.g. for dgemm:

  `dgemm_(transa,...)`

Actually, this depends on the compiler (this applies for all FORTRAN subroutines). GCC uses this convention (lower case and a single underscore at the end), intel also Others might use other naming. According to the documentation for Intel, since it is taken for FORTRAN, it is case insesitive and it may have underscore or not. Trials with gcc give error (only `dgemm_` allowed)

----------------------

## Netlib LAPACK with -O3 optimization when compiling them 
N     | time(s) 
------|-----------
100   | 0.00
500   | 0.15
800   | 0.61
1000  | 1.19
1200  | 2.06
2000  | 10.84

(similar to our Normal-transpose code...)

## ATLAS
N     | time(s) 
------|-----------
5000  | 14.

Much more efficient!

## Intel compiler and MKL
N     | time(s) 
------|-----------
5000  | 1.90
10000 | 7.90

Impressive


# Eigenvalue solver
**********************
Using DSYEV (Double data type; SYmmetric matrices; EigenValue solver)

In C/C++ it outputs the eigenvalues by row (in FORTAN they are returned by column)

---------------------
### <font color='red'>NOTE</font>: UNIX commands

We can re-rerun a command from the hystory by its ID.

 `hystory # returns the hystory`

 `!<ID>`

This runs process with ID=\<ID\>

---------------------

# REFERENCES

Google for `LAPACK cheatsheet`. The website from Colorado University is very useful.

