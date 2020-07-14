
The *Sloan Digital Sky Survey* (or *SDSS*), in operation since the year 2000, has created the largest existing catalog of objects in the sky, including hundreds of thousands of *quasars*. Quasars, or quasi-stellar objects, are objects that appear to be point-like, like stars...but rather than stars, they are the ultra-bright cores of those galaxies in which supermassive black holes are rapidly ingesting material. (As material falls in, it gives off light: the more material, the brighter the quasar, at least roughly. Viewing angle and such matters too.) Quasars do not exist in the local Universe: basically, a galaxy forms, a supermassive black hole forms at its center, that black hole swallows a whole bunch of material in the relative chaotic early days of the Universe (i.e., the quasar "turns on"), things calm down, the quasar "turns off." The black hole remains, but the rate of ingestion of material becomes too low to make the galaxy core abnormally bright.

To use quasars to their fullest statistical potential, we need to know where they are in the Universe. The distance to an object cannot be measured directly, but something that is directly observable is an object's *redshift*.

So here we have to make a slight digression: what is redshift? The short story is that the Universe is expanding, and photons traveling through it have wavelengths that are tied to the expansion. Since the Universe expands appreciably during the perhaps billions of years it takes photons to reach us from an object, the wavelengths of these photons also increase appreciably, making the objects appear redder (hence "redshift"). Redshift is simply the ratio of the observed wavelength of a photon from an object to its wavelength when it was emitted, minus 1. Thus objects in the local Universe have redshift near zero. Quasars have redshifts of 0.7 or more...with the peak of the quasar distribution in redshift space being at approximately 2. A redshift of 2 means that Universe was only about 3.3 billion years old when light was emitted. (It is 13.8 billion years old today.)

Redshifts can be easy to estimate for galaxies. However, the physics of quasars makes redshift determination a bit harder. In this dataset, we only include those quasars whose redshifts were determined by "visual inspection." Visual inspection is laborious: it would be nice to see if we can learn a statistical model that takes in the quasar's brightness in the X-ray, ultraviolet, optical, infrared, and radio regimes, and spits out an accurate and precise redshift estimate.

Anyway, that's your goal.

The data in this directory contains a predictor data frame that has 21 measurements for each of 216,196 quasars:

| variable name | description |
| ------------- | ----------- |
| `ra`,`dec` | right ascension, declination (celestial longitude and latitude) |
| `bal` | an index related to the breadth of the C IV quasar absorption line |
| `mag.[ugriz]` | SDSS photometric magnitudes |
| `ext.r` | Milky Way extinction in the r band (related to dust along the line of sight) |
| `rass` | brightness in the ROSAT All-Sky Survey (X-ray) |
| `fuv`,`nuv` | brightness in two GALEX bands (UV) |
| `mag.[W1,W2,W3,W4]` | magnitudes in four WISE bans (IR) |
| `flux.[Y,J,H,K]` | brightness in four UKIDSS bands (IR) | 
| `flux.first` | brightness at 21 cm wavelengths (radio) |

Note that we do not include `ext.u`, etc., i.e., the extinctions in other SDSS bands, because they are absolutely collinear with `ext.r`. 

The `response` variable is the redshift.

---

Note that this project can go in many directions.

- The initial goal would be to learn a statistical model relating the predictor variables to the redshift.
- One extension would be to incorporate the uncertainties on each of the measurements, which are not included initially to keep the number of predictor variables relatively low.
- One could also go beyond regression methods to estimate the probability density functions for the redshifts given predictors. (This is dubbed *conditional density estimation*.) In regression, we make assumptions about the shape of the conditional densities (usually: they are normal with constant variance), but here you'd estimate the conditional densities themselves.

