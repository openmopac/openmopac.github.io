---
draft: false
title: "Protein tools"
description: "Proteins in MOPAC"
summary: "tools for analyzing and manipulating proteins"
weight: 5
---

MOPAC contains several features designed specifically for proteins.
As suggested by its name, the MOZYME solver was designed to study proton transfer reactions in enzymes.
An atomistic study of proteins such as enzymes needs to start with atomistic structure, which can be large and complicated.
A popular source of protein structure data is the Protein Data Bank (PDB), and MOPAC has tools for processing data from this source and preparing it for MOZYME calculations.
These tools are associated with specific MOPAC keywords, and the simplest of these tools/keywords are summarized below.
See the online MOPAC manual for more detailed information on advanced protein functionality such as transition state searches for enzymatic reactions.

## GEO_DAT

MOPAC can read protein structures that are stored in the PDB file format, usually with a `.pdb` file extension.
Specifically, a PDB file `protein.pdb` file can be read by using the `GEO_DAT="protein.pdb"` keyword instead of inputting the protein structure directly into the MOPAC input file.
In addition to the structure data, MOPAC retains the atom labels from the PDB file.

In recent years, the PDB has switched from the PDB file format to the mmCIF file format with a `.mmcif` file extension, but MOPAC does not directly support the mmCIF file format.

## PDBOUT

This keyword causes MOPAC to print the output structure of a calculation in the PDB file format. As with other output files, the `.pdb` file extension
is appended to the name of the input file. Take care not to overwrite existing `.pdb` files unintentionally.

## RAMA

This keyword causes MOPAC to print the Ramachandra angles (phi, psi, and omega) for the residues of a protein in the `.out` output file.

## RESIDUES

This keyword causes MOPAC to relabel the atoms in a protein with a unique atom label for each atom in an amino acid residue, a 3-letter abbreviation for the residue,
a letter for the polypeptide chain, and a number for the position in the polypeptide.

## RESEQ

This keyword causes MOPAC to reorder the atoms in a protein into a standard PDB sequence.

## ADD-H

This keyword causes MOPAC to remove all of the hydrogen atoms from a structure and add new hydrogen atoms to create chemically sensible closed-shell organic molecules.
Because hydrogen positions in proteins cannot be reliably identified by x-ray crystallography, PDB files often have missing or omitted hydrogen atoms.
There is some unavoidable ambiguity in the assignment of hydrogen atoms, and the `ADD-H` feature was designed and tested with the sensible hydrogenation of proteins in mind.

## SITE

This keyword can be used to adjust the behavior of the `ADD-H` keyword. The simplest use of this keyword is `SITE=(SALT)`, which forces all terminal nitrogen atoms
within 4 Angstroms of a caboxylic acid group to become a salt bridge. This causes the hydrogen and charge assigment of (NH3)+ and (COO)- instead of (NH2) and (COOH).
