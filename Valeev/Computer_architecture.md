# Computer Architecture

Tests in `core/`

***********

Two things to optimize

* Memory access: it is preferable to have less memory traffic, even if we need more computations (we need spatial and time locality in data access)

* Parallelism


*************

## Arithmetic Logic units

* Avoid expensive operations
The latncy associated with divisions are heviear latency than addtions and multiplications. So we need to avoid divisions in our code.

* Avoid branches
Branches (`if`, `for`, ...) are bad for pipeline process, since it introduce pipeline stalls.

* Avoid data dependencies between adjacent instructions
Try that the operate on different variables

* Avoid code composed of one kind of instructions, e.g all floating-point
This is because modern processors can perform different ALU at the same clock cycle

## Vector (data-parallel) processors
Classic vectors machines: Cray, NEF, Fujitsu

Vectorization increase the trhoughput

Possibilities:
* SIMD

The compilers are not very efficient producing vectorization. But there are some C/C++ instructions that
allow to explicitely indicate the vectorization in the code.


## x86 SIMD instructions sets

* Streaming SMD Extensions (SSE)

* Advance Vector Extensions (AVX)
The vector is larger. We can fit 8 ints or 4 doubles (256-bit registers)

In the near future, Extensions of x86 will have 512-bit (8 doubles or 16 ints). In the next year, probably, all computers (including laptops)


## GPU
NVIDIA: Fermi, Kepler (newer)

If you need single precision, you can use a consume card, which are not very expensive. But if
you need double precision, you will need a very expensive card.

---------------
#### Reference:
Computer Architecture: a Quantitative Approach, Henessy and Patterson

----------------

## Distributed-memory multiprocessors
Used MPI programming model

We need fast intercommunication. Nowadays, infiniband is generally used, which have a low latency. Interconnect technologies:

| Technology   |Latency| Cost |
|--------------|-------|------|
| GigE         | 40-50 |  $   |
| Infiniband   | 2-5   |  $$  |




