# GNU debuger: GDB

We need to first compile with the `-g` flag, and without any optimization.

The we can execute gdb on our code. gdb works through some commands, such as:

* `run`: Excecute the program

* `list`: list source code lines close to our position

* (and more...) check the presentation!


------------
### NOTE
A very interesting tool that might be useful for interactive debbuging (also for other things) is `screen`

------------

Runnng gdb (testing with mm/mm executable)

`gdb mm` 

It take us to gdb interactive command line. The workflow then can  be:

1. We first add break points with `break` (the program will also break we there is a bug)

    E.g. `break main` (we go to main, i.e. the main program in C/C++). In general `break <function name>` (or class, type...) or we can spcify the line we want to break in as `break <line number>`. We can examine the code, to see the lines and functions, with `list` at anytime. It will list around the point we are.

    To remove a breakpoint, use `delete`. The breakpoints are numbered starting from 1 (the id is shown when it is created)

2. The we `run` the code. It will stop in the break points. Note that if the program needs arguments, they should be given as run X`.
    
3. We play at every break point with commands such as 
  - `next` goes to next line 

  - `step` follow the program execution flow (i.e. go to the place where a function is defined if it is called)

     With `step` it can find where the functons where defined (even in different files, as far as all is build with the `-g` flag. We can also decided not to compile some part of the code with that flag, if we are not interested on inspecting that part. Once we place the "tip" with step in other different part of the code, `next` will move there. To go back to the previous level: `return`

  - `whatis <variable>` (gives the type)

  - `set <variable>` set the valua for a variable

  - `print` print the value of a variable

  - `where` it gives where we are in the code. If we are `step`ping, it tell us the different levels we are in: i.e. which line in the main funtion (#0) and which line in the called function or class or whatever (#1). And so on if there are more sub-actions. 

4. If we are done in that breakpoint and want to continue to the next one: `continue`

------------
### NOTE: shortcuts

We can call each command by only its initial, i.e `p` = `print`. By clicking return, it will simply execute the last command.

------------

