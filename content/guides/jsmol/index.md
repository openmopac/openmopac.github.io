---
draft: false
title: "Jmol/JSmol visualization"
description: "Jmol/JSmol visualization of MOPAC outputs"
summary: "how to set up and use Jmol/JSmol to visualize the output of MOPAC calculations"
weight: 2
---

One of the simplest ways to visualize MOPAC outputs is by using Jmol and JSmol because MOPAC provides native support for these visualization tools.
For information on obtaining and installing Jmol and JSmol, see the [Jmol/JSmol website](https://jmol.sourceforge.net).

## Jmol

A Jmol-compatible MOPAC output file with the `.mgf` file extension is produced by adding the `GRAPHF` keyword to an input file.
The `.mgf` output file can be opened in Jmol, which displays a ball-and-stick model of the output molecular structure.
Molecular orbital isosurfaces can be viewed by pressing the right mouse button inside the Jmol viewer to open up a menu
and then navigating through the "Surfaces" and "Molecular Orbitals" menu options for a list of MOPAC molecular orbitals to display as isosurfaces.

## JSmol

A JSmol-compatible MOPAC output file with the `.html` file extension is produced by adding the `HTML` keyword to an input file.
For security reasons, modern web browser security prevents the use of local Javascript programs in HTML files.
To use a local copy of JSmol with a MOPAC-generated HTML file, you should activate a local server from an active directory
containing a JSmol installation in the `/jsmol` subdirectory. The HTML files should be located in this active directory or a subdirectory.
If the page is opened directly from disk instead (a `file://` address), the JSmol panel stays empty; MOPAC 23.2.6 and later show a message explaining why instead.
HTML files written by MOPAC 23.2 and earlier load JSmol from `../jsmol/` instead of `/jsmol/`, so they work only when they are exactly one folder below the folder holding `jsmol`.

### Setting up JSmol

Download the latest `Jmol-xx.x.x-binary.zip` from the [Jmol/JSmol website](https://sourceforge.net/projects/jmol/files/latest/download),
open it, open the `jsmol.zip` inside it, and copy the `jsmol` folder out into a folder that sits above the folders where you run MOPAC.
One copy is enough for all of your calculations, at any depth below it:
```
MOPAC/                  <- the local server's root ("active directory")
  jsmol/                <- contains JSmol.min.js
  project1/
    molecule.html
  project2/runs/today/
    test.html
```

### Opening HTML files with the MOPAC JSmol launcher

The MOPAC installers for 23.2.6 and later include a `jsmol-launcher` folder with scripts that do the rest for you.
If you installed MOPAC another way (for example with conda), or have an older version, download the folder from [GitHub](https://github.com/openmopac/mopac/tree/main/jsmol-launcher); the scripts work with any version of MOPAC.
The scripts find the folder holding `jsmol` above the HTML file, start a local server rooted there (or reuse one that is already running),
and open the page in your default browser. No administrator rights are needed, nothing is written into your working folders,
and the server only accepts connections from your own computer.

- **Windows:** drag an HTML file onto `jsmol-launcher\windows\Open_MOPAC_HTML.cmd`, or choose that file under "Open with" for `.html` files.
  `Stop_MOPAC_server.cmd` stops the server. Only PowerShell, which is part of Windows, is used.
- **macOS and Linux:** run `jsmol-launcher/unix/open-mopac-html.sh molecule.html` (requires `python3`); `--stop` stops the server.

If JSmol is kept elsewhere, set the environment variable `MOPAC_JSMOL_ROOT` to the folder containing `jsmol`.
See the `README.md` in the `jsmol-launcher` folder for details.

### Starting a local server by hand

There are many ways to activate a local server. For example, a Python 3 installation can be used to activate a local server with the command:
```
python -m http.server
```
This activates a local server on port 8000, which can be viewed in a web browser at the URL `http://localhost:8000`.
Other software might use a different port by default, and there are usually options to select the port used by the local server.
The file structure of the local server is relative to the activate directory it was activated in.
For example, if an HTML file `molecule.html` is in the active directory, then it can be viewed at `http://localhost:8000/molecule.html`.
If the file is in a `/mopac_data` subdirectory of the active directory, then it can be viewed at `http://localhost:8000/mopac_data/molecule.html`.

When viewed from a web browser, the standard behavior of MOPAC's `.html` output files is to display the output molecule in an interactive JSmol window.
If separate MOPAC calculations were performed using the `HTML` and `GRAPHF` keywords, then the resulting `.mgf` file can be dragged and dropped into
the JSmol window to enable viewing of the molecular orbitals. If a MOPAC calculation is performed with both the `HTML` and `GRAPHF` keywords, then
the HTML file automatically loads the `.mgf` molecular orbital data into the JSmol viewer.
JSmol has the same menu structure as Jmol for displaying the molecular orbitals as isosurfaces.

## JSmol example

As an example, a MOPAC calculation of benzene with Jmol and JSmol output enabled:
```
1SCF GRAPHF HTML
benzene

C  0.0000  1.3970 0
C  1.2098  0.6985 0
C  1.2098 -0.6985 0
C  0.0000 -1.3970 0
C -1.2098 -0.6985 0
C -1.2098  0.6985 0
H  0.0000  2.4810 0
H  2.1486  1.2405 0
H  2.1486 -1.2405 0
H  0.0000 -2.4810 0
H -2.1486 -1.2405 0
H -2.1486  1.2405 0
```
should produce an `.html` file that looks like [this](/benzene.html) when viewed from a local server with JSmol located in the `/jsmol` subdirectory of its root directory.
