---
draft: false
title: "CMake build"
description: "information on how to build MOPAC from source"
summary: "how to download MOPAC source from GitHub and build it with CMake"
weight: 4
---

You can build MOPAC yourself from the source code in [its GitHub repository](https://github.com/openmopac/mopac).
From a Linux shell command prompt, the commands to clone the GitHub repository and enter the root directory is:  
```
git clone git@github.com:openmopac/mopac.git
cd mopac
```
   
MOPAC is built using a CMake 3.x build system with tests orchestrated using CTest.
The minimum required CMake version is presently 3.14.

CMake performs out-of-source builds, with the canonical sequence of Linux shell commands:
```
mkdir build
cd build   
cmake ..   
make
``` 
starting from the root directory of the MOPAC repository. MOPAC should build without any additional options
if CMake successfully detects a Fortran compiler and BLAS/LAPACK libraries. Otherwise, the `cmake ..` command
may require additional command-line options to specify a Fortran compiler (`-DCMAKE_Fortran_COMPILER=...`)   
or the path (`-DMOPAC_LINK_PATH=...`) and linker options (`-DMOPAC_LINK=...`) to link BLAS and LAPACK libraries to the MOPAC executable.
The CTest-based testing also requires an installation of Python 3.x and Numpy that can be detected by CMake.

To build MOPAC with [MolSSI Driver Interface (MDI)](https://molssi-mdi.github.io/MDI_Library/) support enabled, use the CMake command-line option `-DMDI=ON`.

After a successful CMake build, the MOPAC executable and shared libraries will be in the out-of-source build directory (e.g. `/build`).
The executable can then be tested with the shell command `ctest` unless testing has been disable.
Finally, MOPAC can be installed with the shell command `make install`.
