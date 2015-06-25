# VALGRIND
Detects memory leaks

`valgrind <command> <args>`

Very useful, since it traks back to the first place where allocation problem arrises (even if the program do not cause a segfault at this step).

Note that the program will run much slower with valgrind

Example: `debug1/eigenvalue`

`
==20511== Invalid write of size 8

==20511==    at 0x401B56: tred2(int, double**, double*, double*, int) (diag.cc:143)

==20511==    by 0x40132A: diag(int, int, double**, double*, int, double**, double) (diag.cc:60)

==20511==    by 0x400C06: main (eigenvalue.cc:52)

==20511==  Address 0x5a1c178 is 16 bytes after a block of size 8 alloc'd

==20511==    at 0x4C2B800: operator new[](unsigned long) (in /usr/lib/valgrind/vgpreload_memcheck-amd64-linux.so)

==20511==    by 0x400BB3: main (eigenvalue.cc:47)
`

Two components of memory: 

* stack: the memory that the program uses, that knows at compile time. E.g. the space requierd to store a given statically allocated variable

* heap: memory not known at compilation time (dynamically allocated). The program has to ask for it to the system at run time.

valgrind will only detect heap memory leaks.

Possible memory issues are: trying to write/read not allocated memory (`Invalid write` or `Invalid read`) or trying to deallocate already deallocated memory (`Invalid free`)

