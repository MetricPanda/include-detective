# Include Detective

Simple shell script that analyzes the include chain of a C/C++ file or system header.

![](/images/include-detective-windowsh-lean-and-mean.gif)


## How does it work?

Include Detective is a bash script that runs the compiler on a dummy C or C++ file with just an `#include` directive. The `#include` points to the path or system header specified as argument to the script.

The compiler (GCC and Clang family of compilers) is invoked twice with flags `-E` and `-dM`.

The `-E` flag stops compilation after the preprocessing stage, resulting in an output where all headers have been inlined and preprocessor directives and macros expanded.

The `-dM` flag tells the compiler to dump all preprocessor defines (both builtin and the ones defined in the included files).

These outputs are then parsed and statistics printed as you can see above.


## How to use


    Usage: include-detective [options] <file>
    Print include statistics about a C/C++ file or system header

    Options:
      -p     print the preprocessed source instead of
              computing stats
      -d     print the preprocessor defines
      -i     print nested includes
      -h     show this help
      -x     <file> is a C++ file

    Environment variables:
      CC     path to the compiler executable
      CFLAGS compilation flags to pass to the compiler.
              these flags cannot contain filenames or
              output specifiers (e.g. -o)
      MODE   specify MODE=c++ to process as C++

Environment variables can be set on a per-command basis by prefixing the command like so:
`CC=clang CFLAGS="-std=c99 -fno-builtin" stdio.h`

## Why should I use it?

*Include Detective* can be useful when you are looking to eliminate headers in order to **speed up compile times** when using [single translation unit builds](https://en.wikipedia.org/wiki/Single_Compilation_Unit), in favor of [precompiled headers](https://en.wikipedia.org/wiki/Precompiled_header).

Take a look at the blog post [Include Detective: Keep An Eye on Those Includes](https://metricpanda.com/rival-fortress-update-38-include-detective-keep-an-eye-on-those-includes) for more details.


## Installation

### Linux/macOS

1. Clone the repository and `chmod +x` the script to make it executable.
2. Run it passing the path to a source file or a system header file.

### Windows

Haven't tried, but you can probably run it on a Linux-like environment like Cygwin or using the Windows Subsystem for Linux if you are on Windows 10.


## License

[Public Domain](/LICENSE)


