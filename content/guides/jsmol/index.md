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
and then navigating through the "Surfaces" and "Molecular Orbitals" menu options for a list of MOPAC molecular orbitals to display.

## JSmol

A JSmol-compatible MOPAC output file with the `.html` file extension is produced by adding the `HTML` keyword to an input file.
For security reasons, modern web browser security prevents the use of local Javascript programs in HTML files.
To use a local copy of JSmol with a MOPAC-generated HTML file, you should activate a local server from an active directory
containing a JSmol installation in the `jsmol` folder. The HTML files should be located in this active directory or a subdirectory.

There are many ways to activate a local server. For example, a Python 3 installation can be used to activate a local server with the command:
```
python -m http.server
```
This activates a local server on port 8000, which can be viewed in a web browser at the URL `http://localhost:8000`.
Other software might use a different port by default and there are usually options to select the port used by the local server.
The file structure of the local server is relative to the activate directory it was activated in.
For example, if an HTML file `molecule.html` is in the active directory, then it can be viewed at `http://localhost:8000/molecule.html`.
If the file is in a `mopac_data` subdirectory of the active directory, then it can be viewed at `http://localhost:8000/mopac_data/molecule.html`.

When viewed from a web browser, the standard behavior of MOPAC's `.html` output files is to display the output molecule in an interactive JSmol window.
If separate MOPAC calculations were performed using the `HTML` and `GRAPHF` keywords, then the resulting `.mgf` file can be dragged and dropped into
the JSmol window to enable viewing of the molecular orbitals. If a MOPAC calculation is performed with both the `HTML` and `GRAPHF` keywords, then
the HTML file automatically loads the `.mgf` molecular orbital data into the JSmol viewer.
JSmol has the same menu structure as Jmol for displaying the molecular orbitals.

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
should produce an `.html` file that looks like [this](/benzene.html) when viewed from a local server with JSmol located in the `jsmol` subdirectory of its root directory.
