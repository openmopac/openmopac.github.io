---
draft: false
title: "Installation"
description: "further information about stand-alone installer"
summary: "how to install MOPAC using the stand-alone installers"
weight: 1
---

The graphical installer (`.run`, `.dmg`, or `.exe`) is created using the [Qt Installer Framework](https://doc.qt.io/qtinstallerframework/).
It prompts the user for an installation directory and adds the MOPAC executable to the system path.

The compressed archive (`.tar.gz` or `.zip`) contains the MOPAC executable in the `/bin` directory, which depends on shared libraries
contained in the `/lib` directory on Linux/Mac or the `/bin` directory on Windows.
If you want the MOPAC executable to be in your path, then you have to add it yourself using environment or registry variables.

The open-source version of MOPAC does not require a password to activate, unlike the previous commercial versions of MOPAC.

MOPAC installation should be straightforward with a few OS-specific caveats.

## Linux

The Qt Installer Framework may not be compatible with all Linux distributions. While it is primarily meant to be used on a graphical desktop,
the installer can also be run from a Linux command prompt using the syntax:
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

## MacOS

MacOS Gatekeeper might not let you run the installer or MOPAC executable directly at first. To satisfy Gatekeeper, you can right-click an executable in Finder,
select "open", and then acknowledge that you trust the executable in the window that pops up.

Like Linux, MacOS can have `libiomp5` compatibility problems if an old library version is in the shared library path (`DYLD_LIBRARY_PATH`).
However, this problem can be fixed on MacOS by moving the offending directories to the failsafe shared library path, `DYLD_FALLBACK_LIBRARY_PATH`,
which has a lower priority than the RPATH.

The MacOS version of MOPAC is presently built for x86 processors and should run on ARM processors (M*x*) through the Rosetta emulation layer.
Once x86 MacOS builds are no longer possible, MOPAC will switch to native ARM builds and no longer support x86 on Macs.

## Windows

Windows Defender might not let you run the installer or MOPAC executable directly at first. You can acknowledge that you trust the executable by
clicking "more info" and "run anyway" in the Defender window.

