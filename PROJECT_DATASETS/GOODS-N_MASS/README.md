**Predicting the Properties of Galaxies in the GOODS-North Field from Multiwavelength Photometry**

The *Hubble Space Telescope*, or *HST*, has been making the deepest observations of the sky since its launch in 1990. It complements, e.g., the *Sloan Digital Sky Survey (SDSS)*, which has mapped a quarter of the sky but only to relatively shallow depth. One particular *Hubble* program, the Cosmic Assembly Near-Infrared Deep Extragalactic Legacy Survey, or CANDELS, was designed to document galaxy evolution over the first third of the Universe's lifetime by systematically making maps of the deep sky in five different fields of size roughly one square degree each. (Contrast this to the full sky, which measures over 40,000 square degrees.) The CANDELS survey utilized optical and near-infrared observations using *Hubble*'s Advanced Camera for Surveys (ACS) as well as observations further into the infrared using *Hubble*'s Wide-Field Camera (WFC3). The result is the largest catalog of far-away galaxies that has yet been created.

What we observe is brightness in various wavelength bands that are generally denoted with letters such as U or K, etc. (See [this Wikipedia page](https://en.wikipedia.org/wiki/Photometric_system) for more information about how each of the wavelength bands mentioned below maps to actual wavelengths of photons.) What we want to know, however, are galaxy properties such as mass and star-formation rate. Given enough brightness data at enough wavelengths and computer codes that use known physics to map galaxy properties to brightness, one can infer these properties. But can we do just as well using statistical learning? Can we train regression models that map brightness to, e.g., mass directly, without any physics being involved? That's what you'll attempt to discover here.

The predictor data are comprised of two sky coordinates and 13 measurements of brightness at different wavelengths (from the near-ultraviolet regime through the optical regime to the near-infrared) for 13,359 galaxies with estimated masses greater than one million solar masses:

| Variable Name | Description |
| ------------- | ----------- |
| `RA`,`DEC` | Celestial longitude and latitude of galaxy |
| `KPNO_U_FLUX` | Brightness of galaxy as observed in the U band at Kitt Peak National Observatory |
| `LBC_U_FLUX` | ... in the U' band at the Large Binocular Telescope |
| `ACS_(F435W,F606W,F775W,F814W,F850LP)_FLUX` | ... at five different wavelengths (0.435 microns, etc.) using *Hubble*'s Advanced Camera for Surveys |
| `WFC3_(F105W,F125W,F140W,F160W)_FLUX` | ... at four different wavelengths (1.05 microns, etc.) using *Hubble*'s Wide-Field Camera |
| `MOIRCS_K_FLUX` | ... in the K band at the Subaru Telescope |
| `CFHT_Ks_FLUX` | ... in the K<sub>s</sub> band at the Canada-France-Hawaii Telescope |

There are several possible response variables. The one included in the present data is the log-base-10 of the estimated galaxy stellar mass, in units of solar masses. (For example, a "mass" of 9 means one billion solar masses, etc.) Note: because we cannot put galaxies on scales, there is no ground truth here; the true stellar masses are uncertain. However, this is OK; the goal here is to see if we can do just as good a job at predicting masses by applying statistical learning methods to the predictor variables listed above as astrophysicists do using computationally intensive, physics-based computer codes.

Other possible response variables are star-formation rate, specific star-formation rate, galaxy metallicity, etc. Contact me at pfreeman AT cmu DOT edu if you would like me to re-package the data so as to include some of these other variables.

[This paper by Barro et al. (2019)](https://arxiv.org/abs/1908.00569) documents the data included in this dataset. (Note that the data have been preprocessed so as to include only galaxies with estimated masses greater than one million solar masses, to exclude columns with large amounts of missing data, and to ensure that all of the remaining data are "complete," i.e., that there are no missing data remaining.)

