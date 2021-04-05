# pseudopotential

Valence Electron - Noble Gas Atom Pseudopotentials for Atomic Spectral Line Shape Calculations

This Fortran program and accompanying data may be used to compute the long range interaction of a polarizable atom or molecule with an atom with one excited electron.  

While it depends on adjustable parameters, they may be estimated from first principles or refined by matching some states to known first principles calculations or experiments. It returns the eigenstate energies as a function of atomic separation, and for those states gives the decomposition in the isolated atom basis states.  Thus it shows how states mix as a consequence of atomic interactions, and reveals the changes in apparent dipole transition probability for atomic states during collsion.  The resulting long range potentials are more accurate than simply assuming a Van der Waals potential for computing neutral atom collision line broadenign, and are useful as a guide to convergence at long range of *a priori* models.  

## Version

The first version of this code was completed on 1989-04-22 for use with VAX Fortran.  It has been through several versions since then and the one released here 
from 2019-11-28 has been annotated for use with H-He.  

## Features and limitations

* Computes energies and eigenvalues for alkali-noble gas potentials
* Pseudopotential with spherical cutoff
* Induced dipole outside depends on polarizability
* Gombas contact term depends on a perturber electron density parameter
* Fermi contact inside depends on scattering length
* Core-core interaction model is the same for all states and is not included 

## Source

All of the Fortran source code is one file: potnl.f

## Dependencies

This code has its origins in Fortran versions that are now out of date, but it will compile without error on Linux with the Gnu Fortran compiler as of 2021.  See Compile for more information.

The program produces data formatted for use with [Grace](https://plasma-gate.weizmann.ac.il/Grace/).

## Data

Excecution requires files for the state energies, pseudopotential parameters, and the range of atomic separations to be computed.  Examples are provided in the data directory. Links here are to H-He.

### [states.dat](data/hhe/states.dat) 

*   Asymptotic state energies and quantum numbers with the format (5(1x,F10.3))

  *   ENERGY (CM-1)
  *   L
  *   J
  *   M

### [param.dat](data/hhe/param.dat)

*   Parameters defining the potential

  *   ALPHA - Polarizability in A^3
  *   R0 - Cutoff radius for nobel gas
  *   SL - Scatttering length in A (not used in this version)
  *   NS - Number of perturber electrons that scatter valence electron
  *   JVSELECT - Eigenvector selected for listing
  *   NLOW - Lowest state for tabulation

### [range.dat](data/hhe/range.dat) 

*   Range of atomic separations used in the output files

  *   RBEGIN - Starting R in A
  *   RDEL - Delta R in A
  *   NPTS - Number of points to compute



## Compile

As of 2021, Gnu Fortran version 10.1.1 will compile the code with

```
gfortran -o potnl potnl.f

```
with warnings.  This program uses features of older Fortran that have been deprecated in Fortran 2018.
```
Shared DO termination label 
Arithmetic IF statement
```
It may be necessary to rewrite those instances if these features are not available on your compiler.  

## Use

Create one directory with the three requisite data files and excecute potnl from that directory.  


## Output

The program will create two files:

### potnl.dat

* RG (A)
* ENERGY (CM^-1)
* Largest contributions to eigenvectors and percentages

### pseudo.agr

* Grace project file with  8 states from NLOW to NHIGH
* Grace NXY column format RG (A) and ENERGY (CM^-1)


### Documentation

The pdf file in documents describes the physics implemented in this code.  The source code is annotated with programming support.


### References

See the documentation for details about this version of the code and the science on which it is based. 

### License

Distributed under the [MIT License](https://github.com/git/git-scm.com/blob/main/MIT-LICENSE.txt). 


### Contact

[John Kielkopf, Professor of Physics and Astronomy, University of Louisville](https://www.astro.louisville.edu/john_kielkopf)

[jkielkopf@gmail.com](mailto:jkielkopf@gmail.com)

