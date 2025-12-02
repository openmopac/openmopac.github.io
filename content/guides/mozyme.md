---
draft: false
title: "MOZYME solver"
description: "MOZYME fast solver"
summary: "fast solver for closed-shell systems"
weight: 4
---

MOZYME is a fast solver algorithm in MOPAC that accelerates the self-consistent field (SCF) cycle by representing the electronic ground state
with localized molecular orbitals (LMOs) instead of canonical molecular orbitals. MOZYME is faster and uses less memory than the conventional
solver algorithm in MOPAC once the system size exceeds a few hundred atoms. Formally, the solution time of the MOZYME solver scales linearly
in the number of atoms if the number of SCF iterations is independent of system size, while the conventional solver scales cubically.
However, MOZYME will not work for every system and cannot calculate properties of canonical molecular orbitals such as HOMO and LUMO energies.
For a detailed description of the MOZYME solver, see its [implementation paper](https://doi.org/10.1002/(SICI)1097-461X(1996)58:2%3C133::AID-QUA2%3E3.0.CO;2-Z).

The MOZYME solver is activated by adding the `MOZYME` keyword to a MOPAC input file. Many of MOPAC's features are compatible with the MOZYME solver
and require no further changes to the input file. However, MOZYME causes two important changes to a MOPAC calculation. First, a formal Lewis structure
analysis is performed on the input geometry. Based on covalent bonding and shell-filling rules and inter-atomic distances, all atoms are assign
covalent bonds and a formal charge. Once this analysis is complete, MOZYME will try to set the total charge of the system to achieve a closed-shell
electronic configuration. If it is unable to achieve a closed shell, MOZYME will end the calculation. Second, the total charge of a MOZYME calculation
defaults to the total charge determined by the bonding analysis rather than a neutral charge. If a different total charge of `x` is required, then
the `CHARGE=x` keyword also needs to be added to the input file. The MOZYME bonding analysis will then attempt to achieve a closed shell that is
compatible with the total charge constraint.

The MOZYME solver needs the bonding analysis to generate a good initial guess for the LMOs. The LMOs are optimized using pseudodiagonalization,
which usually needs a good initial guess to converge. If you believe that a system has a closed shell but MOZYME fails to detect it, then
you can use the `LEWIS` keyword to provide more details of the bonding analysis for debugging purposes. See the online MOPAC manual for more
information about the MOZYME solver and advanced keywords that can further guide and constrain its bonding analysis.

The MOZYME solver is incompatible with vibrational and excited-state calculations, and polarizability calculations must be static rather than
frequency-dependent. Because the MOZYME solver requires a closed shell, it is limited to restricted Hartree-Fock (RHF) calculations and cannot
perform unrestricted Hartree-Fock (UHF) calculations.
