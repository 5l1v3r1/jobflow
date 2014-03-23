jobflow by rofl0r
=================

this program is inspired by GNU parallel, but has the following differences

 + written in C (orders of magnitude less memory used, a few KB vs 50-60 MB)
 + does not leak memory
 + much faster
 + supports rlimits passed to started processes
 - doesn't support ssh (usage of remote cpus)
 - doesn't support all kinds of argument permutations

basically, it works by processing stdin, launching one process per line.
the actual line can be passed to the started program as an argv.
this allows for easy parallelization of standard unix tasks.

it is possible to save the current processed line, so when the task is killed
it can be continued later.

example usage:
you have a list of things, and a tool that processes a single thing.

    cat things.list | jobflow -threads=8 -exec ./mytask {}

    seq 100 | jobflow -threads=100 -exec echo {}

    cat urls.txt | jobflow -threads=32 -exec wget {}

    find . -name '*.bmp' | jobflow -threads=8 -exec bmp2jpeg {.}.bmp {.}.jpg

run jobflow without arguments to see a list of possible command line options,
and argument permutations.


