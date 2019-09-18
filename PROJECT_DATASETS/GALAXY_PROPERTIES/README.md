
The *Sloan Digital Sky Survey* (or *SDSS*), in operation since the year 2000, has created the largest existing catalog of objects in the sky, including hundreds of millions of galaxies. Galaxies come in a range of shapes and sizes, and they gain weight as they age. We cannot put galaxies on a scale, but we would like to be able to estimate their weights (or, really, masses) given how far away they are, how bright they are, etc. A first goal of this project is to attempt this estimation: can you accurately and precisely predict galaxy masses given galaxy brightness data? (Other possible directions are listed below.)

SDSS collects brightness data in two separate ways: via *photometry*, and via *spectroscopy*. Let's start with the latter: spectroscopy means that the light from an astronomical object is essentially dispersed via a prism (not exactly, but the same idea), and recorded on a charge-coupled device (CCD) with high wavelength resolution (~0.1 nanometers or ~1 Angstrom). This resolution is sufficient to resolve the signatures of atomic transitions (emission and absorption lines), which means that we can estimate the object's *redshift* with high precision.

So here we have to make a slight digression: what is redshift? The short story is that the Universe is expanding, and photons traveling through it have wavelengths that are tied to the expansion. Since the Universe expands appreciably during the perhaps billions of years it takes photons to reach us from an object, the wavelengths of these photons also increase appreciably, making the objects appear redder (hence "redshift"). Redshift is simply the ratio of the observed wavelength of a photon from an object to its wavelength when it was emitted, minus 1. Thus objects in the local Universe have redshift near zero.

Photometric data is essentially extremely low-resolution spectroscopic data. Instead of data spread over thousands of narrow wavelength bins, we have data in five wide wavelength bins. The bins are denoted u, g, r, i, and z, with the first four mapping roughly to "ultraviolet," "green," "red," and "infrared." In contrast with spectroscopic data, photometric data is relatively "cheap and easy" to collect. Thus for every galaxy that has been observed spectroscopically, there are roughly 100 that have only been observed photometrically.

So, back to the project goal. The datasets in this directory contain predictor data frames that have 15 measurements for each of 219,812 galaxies:

| variable name | description |
| ------------- | ----------- |
| `ra`, `dec` | right ascension, declination (celestial longitude and latitude) |
| `e.bv` | extinction (a quantity related to dust along the line of sight) |
| `z`, `z.err` | spectroscopic redshift (and its uncertainty) |
| `mag.[ugriz]`, `mag.[ugriz].err` | photometric magnitudes (and their uncertainties) |

The datasets also contain response data frames that have 4 separate possible response variables:

| variable name | description |
| ------------- | ----------- |
| `mass` | log base 10 of galaxy mass, in solar masses |
| `sfr`  | star-formation rate of galaxy, in solar masses per year |
| `age`  | galaxy "age", related to age of constituent stars, in gigayears |
| `absmag.K` | absolute magnitude of the galaxy in the infrared K band |

See below for a short description of the difference between the two datasets.

How are the response variables measured for these galaxies? Via physics models. This is important to note: we do not have absolute ground truth in our training data. The idea behind doing regression is to see if we can reproduce the mass estimates, et al., that physics models produce, without having to run computationally intensive physics model codes. If the codes are incomplete, there will be systematic error(s) that affect both the response variable values and our estimates of them. There is simply no getting around this issue!

To be a little more clear on what a "physics model" is: since we generally know how balls of gas operate, we generally know what the spectrum of a star will look like. We can then combine stellar spectra together to create an idealized galaxy spectrum, and we can compare different spectra to the observed data to determine which most closely matches what we observe. Take the closest match, and read off the mass, etc.: these are the response variable values.

So now we can return to the issue of why there are two datasets. One, labeled `passive`, is the result of modeling the galaxies as passively evolving, while the other, labeled `starform`, is the result of modeling the galaxies as undergoing bursts of star-formation (due to, e.g., mergers with other galaxies). To be clear: the predictor data frames are *the same* for each dataset, it is simply the response variable values that differ. Ultimately, it would be interesting to know (a) if your models work better with one dataset versus the other, and/or (b) if we can identify whether the galaxies that are "well fit" with, e.g., a passive model are also well fit with a star-forming model.

---

Note that this project can go in many directions. For 36-290, it is sufficient to work through to the initial goal outlined in the first bullet point below.

- As stated above, the initial goal would be to regress `mass` upon the magnitudes, (`ra`,`dec`), and `e.bv`. Why not redshift? Because one would in theory like to be able to apply the model to estimate masses for galaxies for which we only have photometry (and thus for which we do not have a precise redshift estimate). However, comparing and contrasting predictive ability for the no-redshift model versus a model that include redshift would be interesting.
- Once an analysis framework is in place, one could extend the project to predict `sfr`, `age`, and/or `absmag.K`.
- Alternatively, one could go beyond regression methods to estimate the probability density function for `mass` given predictors. (This is dubbed *conditional density estimation*.) In regression, we make assumptions about the shape of the conditional densities (usually: they are normal with constant variance), but here you'd estimate the conditional densities themselves. (And one can use conditional density estimators to estimate bivariate response densities, etc...i.e., one can estimate the joint density for `mass` and `sfr`, etc.)

