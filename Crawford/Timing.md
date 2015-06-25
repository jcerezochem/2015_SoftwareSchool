# TIMING CODE
(within the code, not with gprof)

We review the functions `timer_on("label")` and `timer_off("label")`

These functions are give in the repo (see `timer/` folder). This is a code by the instructor. It is C++, but not using `class` (just `struc`)

-------------
### NOTE
* Wall time: total human time spend (do not care about threads)
* User time: time spend by the application of the used (program). Sum over all threads
* System time: time spend by system operations (allocate memory...)

Note that User time might be longer than Wall time (if threaded).

-----------

The results are similar to the output by psi4. 

The timer need to be a global variable. Note that the timer are not deffined in main(), only the calls to time_on("key") and tome_off("key")

The timer object is passed by address, by a pointer (good to understand global variables in C++). 
In timer.cc, we have the deffinition of the `struc timer` and then an instance of this `struc` but
as a pointer: `struc timer *global_timer` (the variable is called global_timer). Then we have function,
such as `void time_init(void)`, which gets the variable as external: `extern struc timer *global_timer` 
(all functions define the variable as `extern`)