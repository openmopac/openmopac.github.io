---
title: "Download"
description: "Download and installation instructions for MOPAC"
---

The most recent versions of MOPAC are distributed under the Apache 2.0 license.
The recommended citation to MOPAC is presently a software citation to its [Zenodo DOI](https://doi.org/10.5281/zenodo.6511958),
but there will soon be an open-source MOPAC release paper in the Journal of Open-Source Software to replace this.
MOPAC can be obtained through a variety of distribution channels, as discussed below.
The development version of MOPAC is available from its GitHub [repository](https://github.com/openmopac/mopac),
which also includes all official [releases](https://github.com/openmopac/mopac/releases).

## Stand-alone installer

The primary distribution channel for MOPAC over the last few decades has been through a stand-alone installer.
The installer for the latest version of MOPAC is available as a [GitHub release](https://github.com/openmopac/mopac/releases/latest).
The commercial version of MOPAC required a password to activate, but this is no longer necessary for the open-source version.

This distribution is available for three operating systems---Linux, MacOS, and Windows---and as a graphical installer (`.run`, `.dmg`, or `.exe`)
or a compressed archive (`.tar.gz` or `.zip`). The installer will add the MOPAC executable to your system path, which you'll have to do manually
if you use the archive.

Installation should be straightforward with a few OS-specific caveats.

### Linux

The graphical installer is created using the [Qt Installer Framework](https://doc.qt.io/qtinstallerframework/),
which may not be compatible with all Linux distributions. While it is primary meant to be used on a graphical desktop, the installer can also be run
from a Linux command prompt using the syntax:
```
./mopac-x.y.z-linux.run install --accept-licenses --confirm-command --root type_installation_directory_here
```
The minimum glibc version required for the precompiled version of MOPAC on Linux is currently 2.17, but that may increase for future MOPAC versions.

The pre-built MOPAC executables use the RPATH system on Linux to connect with its shared libraries, including the `libiomp5` Intel OpenMP redistributable library.
The `libiomp5` library is not properly versioned, and the recent version used by MOPAC is not compatible with older versions that might also exist on a user's machine.
If a directory containing an old version of `libiomp5` is in the shared library path (`LD_LIBRARY_PATH`), this will override the RPATH system, 
link MOPAC to the wrong library, and cause an error in MOPAC execution. The use of `LD_LIBRARY_PATH` is generally discouraged, and there is no simple workaround 
available. The newer version of `libiomp5` is backwards compatible, so replacing the offending version with the version used by MOPAC should preserve the functionality
of other software that depends on the library.

### MacOS

MacOS Gatekeeper might not let you run the installer or MOPAC executable directly at first. To satisfy Gatekeeper, you can right-click an executable in Finder,
select "open", and then acknowledge that you trust the executable in the window that pops up.

Like Linux, MacOS can have `libiomp5` compatibility problems if an old library version is in the shared library path (`DYLD_LIBRARY_PATH`).
However, this problem can be fixed on MacOS by moving the offending directories to the failsafe shared library path, `DYLD_FALLBACK_LIBRARY_PATH`.

The MacOS version of MOPAC is presently built for x86 processors and should run on ARM processors (M*x*) through the Rosetta emulation layer.
Once x86 MacOS builds are no longer possible, MOPAC will switch to native ARM builds and no longer support x86 on Macs.

### Windows

Windows Defender might not let you run the installer or MOPAC executable directly at first. You can acknowledge that you trust the executable by
clicking "more info" and "run anyway" in the Defender window.

## Conda-forge

[![Anaconda-Server Badge](https://anaconda.org/conda-forge/mopac/badges/version.svg)](https://anaconda.org/conda-forge/mopac)

MOPAC is also distributed on the conda-forge channel of the [Conda package manager](https://anaconda.org/).
If you have Conda installed, then MOPAC can be installed from a command line using the command:
```
conda install -c conda-forge mopac
```

Through Conda, MOPAC supports a wider variety of platforms than the stand-alone installer.

## Linux package managers

[![Linux packaging status](https://repology.org/badge/vertical-allrepos/mopac.svg?columns=2)](https://repology.org/project/mopac/versions)

MOPAC is packaged by many major Linux distributions including [Fedora](https://packages.fedoraproject.org/pkgs/mopac/mopac/) and [Debian](https://tracker.debian.org/pkg/mopac).

## CMake build

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

The CTest-based testing requires an installation of Python 3.x and Numpy that can be detected by CMake.

To build MOPAC with [MolSSI Driver Interface (MDI)](https://molssi-mdi.github.io/MDI_Library/) support enabled, use the CMake command-line option `-DMDI=ON`.

## Docker/Apptainer container

A [container for MOPAC](https://hub.docker.com/r/molssi/mopac220-mamba141) is available on the [MolSSI Container Hub](https://molssi.github.io/molssi-hub/index.html).
This container is compatible with [Docker](https://www.docker.com), [Apptainer](https://apptainer.org), and [Singularity](https://sylabs.io).

## Google Play app

MOPAC is also available as a free Android app in the [Google Play Store](https://play.google.com/store/apps/details?id=cz.m).
