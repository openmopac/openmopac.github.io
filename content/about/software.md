---
draft: false
title: "Software"
description: "MOPAC software ecosystem"
summary: "other software that works with MOPAC"
weight: 99
---

Given MOPAC's age and popularity, there is a lot of software that works with MOPAC in a variety of ways.
To get the most out of MOPAC, you should consider the use of one or more of these programs.
Unless otherwise noted as commercial, the software listed here is free to use for all purposes.


## Graphical User Interfaces (GUIs)

### [Amsterdam Modeling Suite](https://www.scm.com/amsterdam-modeling-suite/) (commercial)

A commercial GUI for a variety of atomistic simulation tools including MOPAC from the developers of the Amsterdam Density Functional (ADF) electronic structure software.

### [Facio](https://zzzfelis.sakura.ne.jp)

A free atomistic simulation GUI with support for MOPAC.

### [Maestro](https://www.schrodinger.com/platform/products/maestro/) (commercial)

A commercial GUI and workflow system for atomistic simulation that has support for MOPAC.

### [MedeA](https://www.materialsdesign.com/medea-software) (commercial)

A commercial GUI focused on simulations of materials that has support for MOPAC.

### [MoCalc2012](https://sourceforge.net/projects/mocalc2012/)

An atomistic simulation GUI built from open-source visualization components JSME, CH5M3D, and Jmol/JSmol with support for MOPAC.

### [Signals ChemDraw](https://revvitysignals.com/products/research/chemdraw) (commercial)

This popular GUI software has gone through multiple names and owners (most recently Chem3D Ultra from PerkinElmer), and it is now developed and sold by Revvity Signals Software.

### [WebMO](https://www.webmo.net) (free/commercial)

WebMO is both a web-browser-based GUI to prepare and visualize molecular calculations
and server-side software to perform these calculations either on your own remote server or using cloud compute.
Many QM and MM simulation engines are available in addition to MOPAC. WebMO is particularly popular for educational purposes, and both free and commercial versions are available.

### [Winmostar](https://winmostar.com/en/) (commercial, but free for students)

A commercial atomistic simulation GUI with support for MOPAC and a free student version.


## Application Programming Interfaces (APIs)

### [ASE](https://ase-lib.org)

A Python package that provides a consistent software environment for atomistic simulation by wrapping many different simulation codes, including MOPAC,
as "Calculators" with a standard interface to a variety of pre and post processing tools. Some of its functionality can also be accessed through a GUI.

### [Cuby](http://cuby4.molecular.cz)

A Ruby package that provides a consistent API for molecular simulations at multiple levels of theory (QM, SQM, MM), including MOPAC. It does not support
periodic systems.

### [MDI](https://molssi-mdi.github.io/MDI_Library/)

The MolSSI Driver Interface (MDI) is a low-level API for direct communication between atomistic simulation software through an engine/driver structure.
"Engines" such as MOPAC provide access to potential energy surfaces and atomic forces, while "drivers" use the engine output to perform more complicated calculations.
For example, a driver can enable molecular dynamics in an engine that doesn't natively support any dynamics.

Note that MOPAC executables not distributed with MDI support enabled. To use MOPAC as an MDI engine, you must build it yourself with the CMake command-line option
`-DMDI=ON`.

### [Mopactools](/mopactools/)

A Python wrapper for MOPAC, for both command-line usage and its native API.

### [Pymopac](https://pymopac.readthedocs.io)

Another Python wrapper for MOPAC, for both command-line usage and its native API.

### [QCEngine](https://molssi.github.io/QCEngine/)

A Python-based API for standardized access to computational chemistry codes including MOPAC.


## Visualization

### [AOMix](https://www.sg-chem.net/aomix/index.html)

A specialized tool for molecular orbital visualization and analysis with support for MOPAC output files.

### [Avogadro](https://avogadro.cc)

An editor and viewer for atomistic structures with limited internal MM-based simulation capabilities. It can export atomistic structures to MOPAC input files.

### [Gabedit](https://gabedit.sourceforge.net/home.html)

Another editor and viewer for atomistic structures with limited internal MM-based simulation capabilities. It can export atomistic structures to MOPAC input files
and also visualize outputs such as molecular orbitals and electron density.

### [JMol/JSMol](https://jmol.sourceforge.net)

Jmol is a Java-based viewer for atomistic structures that can overlay information such as isosurfaces of 3D field data.
JSmol is Javascript-based viewer that enables Jmol functionality within a web browser. MOPAC can generate output files that
are viewable in Jmol and HTML files with an embedded JSmol viewer. See the [Guides](/guides) for further details.

### [Molden](https://www.theochem.ru.nl/molden/)

Another viewer for atomistic structures that can overlay field data such as molecular orbitals, with support for MOPAC output files.


## Applications

### [Antechamber](https://ambermd.org/antechamber/ac.html)

A program in the AmberTools software package that assists in the generation of custom force fields for Amber. It has a MOPAC interface to calculate AM1 partial charges
for use with the AM1-BCC model of partial charges.

### [ChemShell](https://chemshell.org)

Software for QM/MM simulations that can use MOPAC as the QM method. MOPAC support presently appears to be limited to the TCL version of ChemShell.

### [indo-analysis](https://github.com/gieseking-lab/indo-analysis)

Python scripts to post-process INDO/S calculations performed by MOPAC.

### [Molaris-XG](https://laetro.usc.edu/molaris.html) (commercial)

QM/MM simulation software developed by the Warshel research group, which can interface with MOPAC as the QM component of a QM/MM simulation.

### [MRCC](https://www.mrcc.hu/)

Quantum chemistry software with a MOPAC interface that enables the use of MOPAC as a low-level theory in ONIOM calculations.

### [NAMD](https://www.ks.uiuc.edu/Research/namd/)

The Nanoscale Molecular Dynamics (NAMD) software is primarily used for large-scale, parallel molecular dynamics simulations.
As discussed in a [feature paper](https://doi.org/10.1038/nmeth.4638), NAMD now has QM/MM simulation capabilities that include a MOPAC interface for the QM component.

### [Phenix](https://www.phenix-online.org)

Phenix is a Python package for biomolecular structure refinement from crystallography data. MOPAC is used by the Quantum Mechanical Restraints (QMR) feature
to assign molecular structures and protonation states when classical heuristics are unable to produce reliable structures.

### [QCArchive](https://docs.qcarchive.molssi.org)

Python-based database, automation, and workflow software that enables high-throughput computational chemistry calculations. It is compatible with any
computational software that is available through the QCEngine API, which includes MOPAC.

### [RMG](https://rmg.mit.edu)

Reaction Mechanism Generator is an automated system for predicting chemical reaction networks. It uses MOPAC to efficiently estimate molecular heats of formation.

### [SEAMM](https://molssi-seamm.github.io)

A Python-based graphical system for designing and executing complicated workflows for atomistic simulation as a visual flowchart.
MOPAC is available as one of the simulation engines in SEAMM.
