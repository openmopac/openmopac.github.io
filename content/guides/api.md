---
draft: false
title: "Application Programming Interface (API)"
description: "Diskless API for MOPAC"
summary: "C-bound API for basic MOPAC calculations"
weight: 7
---

While MOPAC is usually used as a command-line executable with file-based input and output, this isn't always convenient or performant.
In particular, the parallelism of MOPAC is limited to the multithreading of BLAS and LAPACK operations in conventional MOPAC calculations,
and MOZYME calculations are purely serial. However, the memory usage of MOPAC is usually low, and MOPAC can make use of parallel computing
by running many independent calculations simultaneously. In some computing environments, this trivial parallelism may be limited by disk
access because each MOPAC calculation writes multiple output files to disk.

The main purpose of the MOPAC API is to provide access to basic MOPAC functionality with no use of disk and all input and ouput
passed through data structures. It also provides access to standard disk-based MOPAC functionality as an API call. For better portability,
the API is bound to C so that its shared library symbols are not compiler dependent. Fortran compilers are not application binary interface (ABI)
compatible, so they generate libraries with compiler-dependent symbols.

Because the MOPAC API is bound to C, its native calling language is C. However, Python and Fortran API wrappers are available.
For basic examples of C and Fortran API usage, see the [MOPAC GitHub repository](https://github.com/openmopac/mopac/tree/main/examples).

## Python

The easiest way to use the MOPAC API is through Python. Two Python packages with API wrappers are available: [Mopactools](/mopactools/)
and [Pymopac](https://pymopac.readthedocs.io). Both of these packages are available on PyPI and Mopactools is also available on the conda-forge channel of Conda.
See their documentation for further details of use.

## C

The C-bound MOPAC API is fully described by its [C header file](https://github.com/openmopac/mopac/blob/main/include/mopac.h).

The `run_mopac_from_input` function initiates a standard disk-based MOPAC calculation using the input file specified by the string argument of the function.
The `get_mopac_version` function writes the MOPAC version string to the string argument of the function.

The main API calls have the syntax `solver_calc`. `solver` is `mopac` for conventional MOPAC calculations and `mozyme` for fast MOZYME calculations.
`calc` is `scf` for standard self-consistent field (SCF) calculations at a fixed geometry, `relax` for geometry relaxation to a local minimum of heat,
and `vibe` is a vibrational calculation from a relaxed geometry.

Each of the main API calls has three arguments that are data structures for input and output. The first argument is `mopac_system`, which is an input
data structure describing the geometry of an atomistic system and specifying the MOPAC calculation to be performed on it. The second argument,
`mopac_state` or `mozyme_state`, is solver dependent and describes the electronic ground state. The `solver_state` structure is used as input to
specify the initial electronic ground state of the SCF cycle, and it is also used as output to record the final electronic ground state of the calculation.
The `solver_state` input can be assigned a trivial value, `mopac_state.mpack = 0` or `mozyme_state.numat = 0`, to use MOPAC's default initialization
of the electronic ground state. The third argument is `mopac_properties`, which is an output data structure containing the main physical properties
calculated by MOPAC.

MOPAC internally allocates the memory for the `solver_state` and `mopac_properties` structures, there are API calls to deallocate this memory in a consistent manner.
For custom initializations of `solver_state`, the memory within the data structure must be allocated by their corresponding API calls for memory allocation
because API calls must be able to deallocate this memory when updating `solver_state` for output.
The arrays in `solver_state` are allocated memory according to the sizes specified in their corresponding size variables.

## Fortran

The Fortran wrapper for the MOPAC API is fully described by its [Fortran module file](https://github.com/openmopac/mopac/blob/main/include/mopac_wrapper.F90).
The `mopac_api_f` module contains subroutines and derived types that mirror the functions and structures of the C API with `_f` appended to each name.
There are no Fortran API calls for memory allocation and deallocation because memory issues are handled internally by the Fortran wrapper.
Also, the wrapper converts from 0-based indexing to 1-based indexing, from C-style strings to Fortran-style strings, and from C pointers to Fortran arrays.

For ABI compatibility, you must compile `mopac_wrapper.F90` and `mopac_wrapper_internal.F90` with the same compiler as the calling Fortran program.
However, the MOPAC shared library does not need to be compiled with the same compiler, and a pre-built library can be used with the Fortran API wrapper.
