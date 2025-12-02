---
draft: false
title: "Periodic systems"
description: "MOPAC calculations of periodic systems"
summary: "additional details for periodic boundary conditions"
weight: 3
---

The specification of periodic boundary conditions in MOPAC is very simple.
Each translation (lattice) vector of the system is specified at the end of the list of atomic coordinates.
These vectors are parsed like atomic coordinates, with `Tv` specified as the element symbol followed by the real-space Cartesian components
of the vectors in units of Angstroms. The dimensionality of the periodic system is inferred by the number of vectors specified.

The main MOPAC program does not have Brillouin zone sampling implemented. It performs periodic calculations only at the Gamma point of the Brillouin zone,
which corresponds to simple periodic boundary conditions for the electronic orbitals. MOPAC has a companion program named BZ that can perform Brillouin zone
sampling, but it is presently a Windows-only program that depends on a very old Fortran graphics library for visualization. In its present form, BZ cannot
export band structure data in a convenient format for analysis.

With Gamma-point-only calculations, the only way to converge finite-size effects is to expand the unit cell into a supercell. MOPAC has some safeguards
that prevent periodic calculations from running if the unit cell is too small, but there may still be significant finite-size effects if an atom is
directly correlated with its periodic image. MOPAC users should check finite-size convergence of periodic calculations.
For example, a simple polyhydroacene polymer input file with one monomer:
```
LET DDMIN=0.0
polyhydroacene polymer
one monomer per unit cell
C  0     1.49  0
C  0    -1.49  0
C  1.27 -0.68  0
C  1.27  0.68  0
H  0     2.13  0.89
H  0     2.13 -0.89
H  0    -2.13  0.89
H  0    -2.13 -0.89
Tv 2.54  0     0
```
will have its unit cell erroneously collapse during the geometry relaxation.
A supercell with two monomer units:
```
LET DDMIN=0.0
polyhydroacene polymer
two monomers per unit cell
C  0     1.49  0
C  0    -1.49  0
C  1.27 -0.68  0
C  1.27  0.68  0
H  0     2.13  0.89
H  0     2.13 -0.89
H  0    -2.13  0.89
H  0    -2.13 -0.89
C  2.54  1.49  0
C  2.54 -1.49  0
C  3.81 -0.68  0
C  3.81  0.68  0
H  2.54  2.13  0.89
H  2.54  2.13 -0.89
H  2.54 -2.13  0.89
H  2.54 -2.13 -0.89
Tv 5.08  0     0
```
does not collapse upon geometry relaxation and produces a translation vector of length 2.506 A for the elementary unit cell.
However, it produces a heat of formation of 12.057 kcal/mol per elementary unit cell, which is far from convergence.
A three-monomer unit cell results in 2.514 A and 6.232 kcal/mol, and a four-monomer unit cell results in 2.511 A and 5.660 kcal/mol.
The converged values for a very large unit cell are 2.515 A and 5.545 kcal/mol.
Finite-size convergence of periodic systems can depend on both the system and property of interest.

## Practical considerations

MOPAC is tested but not trained on periodic systems, so its accuracy depends on the transferability of models from molecules to materials.
This transferability is best for periodic systems with a molecular character, such as molecular crystals, polymers, and metallorganic frameworks.
MOPAC also describes ionic crystals well, since they are mainly governed by electrostatics and ionic radii determined by interatomic repulsion terms.
MOPAC's description of metals and semiconductors is sensitive to the valence of the consistuent atoms relative to the common valences contained in MOPAC's training data.
Alkali, alkali earth, and transition metals mostly occur in MOPAC's training data as cations with organic ligands, therefore valence electrons on these
atoms that participate in delocalized energy bands may not be represented at all in the training data.
In contrast, MOPAC has a very robust, transferable model of carbon that transfers well to a variety of carbon-based crystals and nanostructures.
All applications of MOPAC to periodic systems should be validated against experimental data or higher levels of theory.

Just as with molecules, the semiempirical models in MOPAC are primarily designed to describe heats of formation, equilibrium geometries, and other structural properties.
Electronic properties such as band structures are also produced by these models, but they are much more loosely constrained by experimental data.
The only training data that directly constrains electronic properties are dipole moments and ionization potentials of molecules, with a heavy emphasis on organic molecules.
Thus, MOPAC should be more accurate for describing electronic properties of carbon-based materials than any other periodic systems.
However, MOPAC tends to overestimate electronic band gaps because its model is based on Hartree-Fock calculations
that are known to overestimate band gaps in first-principles electronic structure calculations.
For example, the PM7 band gap of diamond is approximately 10 eV, the experimental value is approximately 5.5 eV,
and the first-principles Hartree-Fock value is approximately 12.6 eV.
