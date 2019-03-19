# ERGO

This is a distribution of software that comes with the book [Programming Cognitive Robots](http://www.cs.toronto.edu/~hector/pcr.html) by Hector Levesque.  It comes with absolutely no guaranties
or support.  Also, do read the copyright notice.

This directory contains all the files and directions for running the ERGO
system as well as a number of ERGO programs. It contains the following:

* `README.txt`: This file
* `history.txt`: A list of updates and fixes to the software
* `ergo-sheet.pdf`: A one page summary of the ERGO system
* `install.txt`: Instructions on installing ERGO
* `System/`: All the system files
* `Examples/`: Some example ERGO programs
* `Projects/`: Three larger ERGO programs
* `Servers/`: Programs to be run in conjunction with ERGO

Each subdirectory will contain its own explanatory README file.

The original collection of files was put together on **March 17, 2019**.

This describes how to setup and run the ERGO system.

## INSTALL

### INSTALLATION OF RACKET

See http://racket-lang.org/. You can test that things are working with

     > racket -e '(+ 3 4)'
     7

### INSTALLATION OF ERGO

1. First, put all the files in the `Ergo/System/` directory somewhere convenient, away from user ERGO programs.  On a Mac, a reasonable choice is to create `~/Library/Application Support/Ergo/` and put them there.

2. Then find out where Racket keeps user-defined collections.  It's the first element of "`(current-library-collection-paths)`":

       > racket -e '(car (current-library-collection-paths))'
       #<path:/Users/hector/Library/Racket/5.2/collects>

3. Create the user `/path/to/collects/` directory from (2) if needed, and a new subdirectory inside it called "`ergo`".

4. Put a file called `main.ss` in the `ergo/` directory from step (3).  It should contain just the following three lines:

       (module main racket
         (require (file "/path/to/implementation/full-system.scm"))
         (provide (all-from-out (file "/path/to/implementation/full-system.scm"))))

   where the `/path/to/implementation/` is the directory from step (1) above.  

5. Test that ERGO is correctly installed:

     > racket -l ergo -e '(ergo-do :nil)'
         Loading ERGO v1.5 (Mar 2018) in Racket 5.2 ...
     '()


## RUNNING ERGO 

(and do see Chapter 2 of the book)

1. To access ERGO interactively:

       racket -l ergo -i

   From there, the primitive functions like `define-fluents` and `ergo-do` can be used.  Files containing other definitions can be loaded with `include`.

2. To run interactively after loading an ERGO file myfile.scm:

       racket -l ergo -i -f myfile.scm 
       
    Other files can be loaded using "include" within myfile.scm.

3.- To load an ERGO file myfile.scm and then evaluate an expression `expr`:

       racket -l ergo -f myfile.scm -e 'expr'

4- To load an ERGO file myfile.scm and then evaluate (main)

       racket -l ergo -f myfile.scm -m
