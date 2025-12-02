---
draft: false
title: "Basic usage"
description: "Basic usage of MOPAC"
summary: "the basic use and functionality of MOPAC"
weight: 1 
---

MOPAC is primarily a command-line program that requires an input file to be specified on the command line.
The input file specifies the atomic coordinates of a molecule or material and optionally a set of keywords that modifies the behavior of MOPAC.
Once MOPAC is finished a calculation, it will produce one or more output files summarizing the results of the calculation.

The generic syntax to run MOPAC on a command prompt is:
```
path/to/mopac/executable path/to/input/file
```
If the MOPAC executable is in your computer's system path and the input file is in the working directory, then the syntax is:
```
mopac molecule
```
for an input file named `molecule`. On Windows, you can also drag and drop an input file onto the MOPAC executable as an alternative to using the DOS command line.

Unlike most command-line programs, MOPAC places output files in the same directory as the corresponding input file rather than in the working directory.

The MOPAC input file does not have a required file extension, and the input file name is used as the base name for the output files with various file extensions added.
The main output file has the `.out` extension, and an archival output file has the `.arc` extension.
Some file extensions will be stripped from the input file before assigning the base name of the output file.
These recognized input file extensions are `.mop`, `.dat`, and `.arc`, without case sensitivity.
For example, the input files `molecule` and `molecule.mop` will both produce an output file named `molecule.out`.

An input file with the extension `.arc` is assumed to be the archival output file of a previous MOPAC calculation.
Archival output files have a valid MOPAC input file appended to the end, and MOPAC will ignore the rest of the `.arc` input file and run this appended input file.

## Input file format

The MOPAC input file has a simple structure that is sensitive to line breaks but insensitive to white space.
The basic layout of a MOPAC input file is:
```
keyword line
first comment line
second comment line
first atomic coordinate
second atomic coordinate
...
last atomic coordinate
```
The keyword line is a list of keywords separated by whitespace, the two comment lines are ignored by MOPAC, and the remaining lines describe the geometry of an atomistic system.
The most common way to format atomic coordinates is the element symbol followed by the Cartesian coordinates along the x, y, and z axis in units of Angstroms.
For example, the MOPAC input file for a calculation of methane is:
```
1SCF GRADIENTS CHARGE=0
^^^ keyword line
vvv atomic coordinates
C 0 0 0
H 0.63 0.63 0.63
H 0.63 -0.63 -0.63
H -0.63 0.63 -0.63
H -0.63 -0.63 0.63
```
This basic formatting of the MOPAC input file is directly compatible with the `.xyz` file format by inserting a keyword line at the top of the file,
above the line specifying the number of atoms.
Note that a few advanced keywords also require extra lines of information in the input file after the last atomic coordinate is specified.
MOPAC is very flexible in reading the atomic coordinates and will understand multiple variations to this basic format.
For example, each atom can be assigned a label in parentheses immediately following the element symbol, and a 0/1 logic flag can be added after each Cartesian coordinate to specify
whether or not it should be optimized. MOPAC can also read geometries in Z-matrix format and a hybrid mix of Z-matrix and Cartesian coordinates.
Consult the manual for more information on input file formats.

## Common keywords

MOPAC does not require any keywords to function. Its default behavior without keywords is to perform a geometry relaxation using the PM7 model.
This will make a sequence of adjustments to the geometry of the input system to find the local minimum of its heat of formation.
The heat of formation calculated by MOPAC is relative to a decomposition into isolated elements in thermodynamic equilibrium at 25°C.
By default, MOPAC assumes that a system is in vacuum and has a neutral charge and minimum total spin.
Keywords can then be used to adjust (1) the atomistic system, (2) the type of calculation, and (3) the amount of output.
The most commonly used keywords are listed below. Consult the online MOPAC manual for a more complete description of each keyword and a complete list of keywords.

### 1SCF

This keyword performs a self-consistent field (SCF) calculation on the input geometry and returns the result.
It suppresses MOPAC's default behavior of performing a geometry relaxation on the input geometry.
This is useful for understanding the properties of a system at a non-equilibrium geometry.

### GRADIENTS

This keyword requests the calculation of atomic forces. Forces are calculated by default but suppressed by the `1SCF` keyword.
The use of both `1SCF` and `GRADIENTS` enables the calculation of atomic forces at non-equilibrium geometries.

### CHARGE

This keyword specifies the total electric charge of a system in elemenentary units of charge.
For example, `CHARGE=1` removes an electron from a system and `CHARGE=-1` adds an electron to a system.

### MS

This keyword specifies the total electronic spin of a system in elementary units of spin.
For example, `MS=0` is a singlet, `MS=0.5` is a doublet, and `MS=1` is a triplet.

### UHF

This keyword forces MOPAC to perform an unrestricted Hartree-Fock (UHF) calculation in which alpha and beta electronic orbitals are allowed to be different.
MOPAC's default behavior is to perform a UHF calculation for systems with an odd number of electrons and a restricted Hartree-Fock (RHF) calculation for systems
with an even number of electrons.
This default behavior will cause an error for even-electron systems with an `MS=x` keyword for non-zero values of `x` unless the `UHF` keyword is used.

### AM1, PM3, PM6, PM6-D3H4, PM7, PM6-ORG, etc.

By default, MOPAC uses the PM7 model for all calculations because it is the most general-purpose and transferable model available.
The names of other models can be used as keywords to specify their use instead of PM7.
Consult the manual for the full list of semiempirical models available in MOPAC.

### EPS

This keyword activates the COSMO implicit solvent model.
The syntax for this keyword is `EPS=x`, where `x` is the static dielectric constant of the solvent.
A commonly used value is `EPS=78.4`, which is the dielectric constant of water at 25°C.

### PULAY

This keyword causes MOPAC to use Pulay's direct inversion in the iterative subspace (DIIS) algorithm in the SCF cycle.
MOPAC's default SCF mixing algorithm is often the fastest for simple systems, but DIIS is usually more robust.
DIIS can sometimes converge when the default algorithm fails, and it can be faster when the default algorithm causes slow convergence.

### PL

This keyword causes MOPAC to print diagnostic information about each iteration of the SCF cycle in the output file.
If a MOPAC calculation appears to be frozen, then this keyword can be used to check if a convergence failure of the SCF cycle is the cause.
For chemically well-posed systems that are expected to have a closed electronic shell, poor convergence of the SCF cycle may indicate an unphysical geometry, charge, or spin.

When `PL` indicates an SCF convergence problem, the most likely simple solution is to add the `PULAY` keyword.
If `PULAY` does not help, then consult the manual for more SCF options including use of the `OLDENS` keyword to specific a custom input density matrix.

### DISP

This keyword causes MOPAC to print a more detailed decomposition of the heat of formation in the output file.
This includes a list of hydrogen bonds, a "total energy", an "electronic energy", and a "core-core repulsion".
Note that this energy decomposition comes from an artificial partitioning of the semiempirical model into components.
These energy components do not have a direct physical meaning, although they may have some correlation with physical properties.

### AUX

This keyword causes MOPAC to print an extra formatted output file with the `.aux` file extension.
The `.aux` file was designed to be more machine readable than the main `.out` output file. The `.aux` file has the delimiter:
```
 START OF MOPAC PROGRAM
...
 END OF MOPAC PROGRAM
```
MOPAC input files can be concatenated, and MOPAC will perform the corresponding calculations in sequence.
Multiple calculations can use the `AUX` keyword, and each calculation will be reported in the `.aux` file with the delimiter:
```
 START OF MOPAC FILE
...
 END OF MOPAC FILE
```
A `#` as the first non-space character on a line in the `.aux` file denotes a comment.
Each scalar quantity is printed with the syntax:
```
 NAME=VALUE
```
Each vector quantity is printed with the syntax:
```
 NAME[N]=
 VALUE_1 VALUE_2 ... VALUE_N
```
where values may be separated by both whitespace and line breaks.
The specific quantities printed in the `.aux` file and their numerical precision depend on details of the MOPAC calculation
and can be modified by arguments of the `AUX` keyword.

### FORCE

This keyword causes MOPAC to calculate vibrational modes and frequencies using isotropically averaged atomic masses.

### POLAR

This keyword causes MOPAC to calculate the polarizability and first and second hyperpolarizabilities at a specified frequency.
The syntax `POLAR` specifies a static calculation, and the syntax `POLAR(E=x)` specifies a calculation at a frequency of `x` eV.

### THERMO

This keyword causes MOPAC to perform a thermodynamic analysis in the gas phase. This analysis is only valid if the input system is a single, rigid molecule.
The semiempirical models in MOPAC directly generate the heat of formation at 25°C, and the evaluation of thermodynamic properties at other temperatures is
based on a vibrational analysis and a harmonic approximation of vibrational contributions to the free energy.
