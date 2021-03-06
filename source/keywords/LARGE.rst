.. _LARGE:

``LARGE``
=========

Most of the time the output invoked by keywords is
sufficient.\ ``LARGE`` will cause less-commonly wanted, but still
useful, output to be printed. ``LARGE`` increases the amount of output
generated by the keywords\ ``AUX, ENPART, GEOCHK``, ``DCART``, and
``MECI``.

When ``AUX`` is specified, ``LARGE`` will cause all M.O.s to be printed;
the default is the20 around the HOMO-LUMO gap.

When ``COMPFG`` is specified, ``LARGE`` will cause all coordinates to be
printed; the default is the first 5 atoms.

When ``DCART`` is specified, ``LARGE`` will cause all derivatives in a
solid to be printed; the default is the central unit cell only.

When ``DERNVO`` is specified, ``LARGE`` will cause details of the
non-variationally optimized derivatives to be printed.

When ``FMAT`` is specified, ``LARGE`` will cause details of the
construction of the Hessian to be printed.

In a ``FORCE`` calculation, ``LARGE`` will cause the force-constants to
be printed. The default is to print the normal coordinates only.

When ``MECI`` is specified, ``LARGE`` will cause details of the
multi-electron configuration interaction calculation to be printed. This
includes the secular determinant and State vectors.

To save space, ``DRC`` and ``IRC`` outputs will, by default, only print
the line with the percent sign. Other output can be obtained by use of
the keyword ``LARGE``, according to the following rules:

.. raw:: html

   <div align="center">

+-----------------------+-----------------------+-----------------------+
| **``LARGE``**         | **   **               | Print all internal    |
|                       |                       | and Cartesian         |
|                       |                       | coordinates and       |
|                       |                       | Cartesian velocities. |
+-----------------------+-----------------------+-----------------------+
| **``LARGE=1``**       |                       | Print all internal    |
|                       |                       | coordinates.          |
+-----------------------+-----------------------+-----------------------+
| **``LARGE=-1``**      |                       | Print all internal    |
|                       |                       | and Cartesian         |
|                       |                       | coordinates and       |
|                       |                       | Cartesian velocities. |
+-----------------------+-----------------------+-----------------------+
| **``LARGE=n``**       |                       | Print every *n*'th    |
|                       |                       | set of internal       |
|                       |                       | coordinates.          |
+-----------------------+-----------------------+-----------------------+
| **``LARGE=-n``**      |                       | Print every *n*'th    |
|                       |                       | set of internal and   |
|                       |                       | Cartesian coordinates |
|                       |                       | and Cartesian         |
|                       |                       | velocities.           |
+-----------------------+-----------------------+-----------------------+

.. raw:: html

   </div>

To reduce output, do not use ``LARGE``.
