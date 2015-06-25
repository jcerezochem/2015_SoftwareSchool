# PROFILING
(See the tests in `mm_profile`)

The code need to be compiled with the `-pg` flag. All parts of the code we want to test need to have this flag 
(also libs if we want to profile them). And then, we need to run it, and a new file `gmon.out` will appera.

This file is read with

`gprof <binary name>`


This tools is used to understand which parts of the code will benefit more from optimization.











