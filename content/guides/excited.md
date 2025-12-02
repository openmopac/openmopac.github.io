---
draft: false
title: "Excited states"
description: "Excited states in MOPAC"
summary: "how to calculate electronic excitations"
weight: 6
---

MOPAC can calculate electronic excitations using both its native thermochemistry (PM*x*) models and also Zerner's INDO/S (ZINDO) model.
Each option has a different set of advantages and limitations. The PM*x* models provide a baseline potential energy surface from which
to study excited-state potential energy surfaces. However, only atomic excitation energies are in the PM*x* training data, so their
accuracy for delocalized electronic excitations relies on model transferability. The INDO/S model is trained primary on electronic
excitation data of molecules, but it can only predict vertical excitation energies and does not provide access to a complete
excited-state potential energy surface.

All of MOPAC's excited state functionality is based on the configuration interaction (CI) method, with a variety of options for specifying
the set of active configurations in the CI calculation. See the online MOPAC manual for a complete description of these CI options.

For a PM*x* calculation, the simplest way to perform an excited-state calculation is to add the keywords `MECI C.I.=x ROOT=y` to a MOPAC input file.
The `MECI` keyword prints information about the CI calculation in the `.out` output file, `C.I.=x` requests a CI active space constructed
from the *x*/2 (rounded up) highest-energy occupied orbitals and the *x*/2 (rounded down) lowest-energy virtual orbitals, and
`ROOT=y` uses the *y*th lowest-energy state of the CI calculation to define the excited-state potential energy surface.

The simplest way to perform an INDO/S calculation is to add the keywords `INDO C.I.=x` to a MOPAC input file. The `INDO` keyword prints information about
the INDO/S calculation in the `.out` output file, and `C.I.=x` requests a set of active configurations for CI by exciting the lowest energy configuration
with single-electron excitations from the *x*/2 (rounded down) highest-energy occupied orbitals to the *x*/2 (rounded up) lowest-energy virtual orbitals.
Note that the `C.I.` keyword does not have consistent behavior between the INDO and MECI features.
