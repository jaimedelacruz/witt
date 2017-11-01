# Mihalas / Wittmann EOS and background opacity package (from Kurucz)
Written by J. de la Cruz Rodriguez (ISP-SU 2017).

This python package includes a very simple equation of state
originally proposed by Mihalas (1970) and later improved by
Wittmann (1975?). Background opacities can be automatically
computed at a given array of wavelengths.

This EOS considers in detail H, H+, H- and H2, no other molecules.
The purpose of this package is to provide the user with
a simple EOS that can be used to play with toy models or to
compute electron densities / pressure in LTE.

All units in CGS.

The same implementation is found in the SIR code (Fortran) and
in NICOLE (Fortran).

Dependencies:
* It requires a pf_Kurucz.input containing the partition function data.
* Numpy

Usage:
```python
import witt
eos = witt.witt()

temp = 5000.
Pgas = 10000.

Pe = eos.pe_from_pg(temp,Pgas)
rho= eos.rho_from_pg(temp, Pgas)
```
But if we know rho instead of pgas:
```python
rho = 3.e-7

Pgas= eos.pg_from_rho(temp, rho)
Pe  = eos.pe_from_rho(temp, rho)
```
Or if we only know the electron pressure:
```python
Pe = 7.0
Pgas= eos.pg_from_pe(temp, Pe)
rho  = eos.rho_from_pe(temp, Pe)
```

Remember that Pgas is the total gas pressure and it includes the electron pressure. To compute the particle density and the electron pressure, we can use the ideal gas equation: P = n B T:
```python
Na = (Pgas - Pe) / (eos.BK * temp)
Ne = Pe          / (eos.BK * temp)
```

Finally, background opacities can be obtained for and array of wavelengths
in Angstroms:
```python
wav = np.float64([5000., 6000.])
alpha = eos.contOpacity(temp, Pgas, Pe, wav)
```