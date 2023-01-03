# SFF (Stellar Spectral Factory)

**SSF** constructs the interpolation approach based on the Stellar LAbel Machine (SLAM)
which is a data-driven method proposed by
[Zhang et al. 2020a](https://ui.adsabs.harvard.edu/abs/2020ApJS..246....9Z/abstract) and 
[Zhang et al. 2020b](https://ui.adsabs.harvard.edu/abs/2020RAA....20...51Z/abstract).
**SSF** aims to provide an empirical stellar spectral predictor with a wide coverage of stellar parameters
trained on the ATLAS-A library ([Ji et al. submitted to ApJS]()) which contains spectra 
from O type to M type. 

**SSF** consists of 4 sub-models
1. `SSF-N(Teff, logg, [M/H])`: mainly covers the parameter space such that Teff from 3700 to 8700 K, 
`log g` from 0 to 6 dex and `[M/H]` from - 1.5 to 0.5 dex. 
2. `SSF-gM(Teff, [M/H], 1)` covers M giant stars with `Teff` from 3520 to 4000 K and `[M/H]` from - 1.5 to 0.4 dex.
3. `SSF-dM(Teff, [M/H], 0)` covers M dwarf stars with `Teff` from 3295 to 4040 K and `[M/H]` from -1.0 to 0.1 dex. 
4. `SSF-B(Teff, MG)` mainly covers the hot stars with `Teff` from 9000 to 24000 K and `MG` from -5.2 to 1.5 mag. 

where
- `Teff` is the effective temperature
- `logg` is the logarithm of the surface gravity
- `[M/H]` is the overall metallicity
- `MG` is the absolute magnitude in `G` band

# How to use SFF models
1. Download the trained SLAM models from https://nadc.china-vo.org/res/r101182/
2. Load model with the following `Python` code And then can use the code bellow to predict the normalized flux of spectra. 

```python
import joblib

SSFN = joblib.load("SSF-N.z") # SSF-N
Flux = SSFN.predict_spectra([Teff, logg, [M/H]])

SSFgM = joblib.load("SSF-gM.z") # SSF-gM
Flux = SSFgM.predict_spectra([Teff, [M/H], 1])

SSFdM = joblib.load("SSF-dM.z") # SSF-dM
Flux = SSFdM.predict_spectra([Teff, [M/H], 0])

SSFB = joblib.load("SSF-B.z") # SSF-B
Flux = SSFB.predict_spectra([Teff, MG])
```

# Requirements
1. Python 3.9
2. `joblib`
3. `scikit-learn==1.2.0`
4. `astroslam==1.2022.1228.1` (install `astroslam` with `pip install -U astroslam`)
