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

Finally, background opacities can be obtained for and array of wavelengths
in Angstroms:
```python
wav = np.float64([5000., 6000.])
alpha = eos.contOpacity(temp, Pgas, Pe, wav)
```