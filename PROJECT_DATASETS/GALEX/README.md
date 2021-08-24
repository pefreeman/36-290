**Predicting Quasar Redshifts Using UV and Optical Photometry**

The *Sloan Digital Sky Survey* (or *SDSS*), in operation since the year 2000, has created the largest existing catalog of objects in the sky, including hundreds of thousands of *quasars*. Quasars, or quasi-stellar objects, are objects that appear to be point-like, like stars...but rather than stars, they are the ultra-bright cores of those galaxies in which supermassive black holes are rapidly ingesting material. (As material falls in, it gives off light: the more material, the brighter the quasar, at least roughly. Viewing angle and such matters too.) Quasars do not exist in the local Universe: basically, a galaxy forms, a supermassive black hole forms at its center, that black hole swallows a whole bunch of material in the relative chaotic early days of the Universe (i.e., the quasar "turns on"), things calm down, the quasar "turns off." The black hole remains, but the rate of ingestion of material becomes too low to make the galaxy core abnormally bright.

To use quasars to their fullest statistical potential, we need to know where they are in the Universe. The distance to an object cannot be measured directly, but something that is directly observable is an object's *redshift*.

So here we have to make a slight digression: what is redshift? The short story is that the Universe is expanding, and photons traveling through it have wavelengths that are tied to the expansion. Since the Universe expands appreciably during the perhaps billions of years it takes photons to reach us from an object, the wavelengths of these photons also increase appreciably, making the objects appear redder (hence "redshift"). Redshift is simply the ratio of the observed wavelength of a photon from an object to its wavelength when it was emitted, minus 1. Thus objects in the local Universe have redshift near zero. Quasars have redshifts of 0.7 or more...with the peak of the quasar distribution in redshift space being at approximately 2. A redshift of 2 means that Universe was only about 3.3 billion years old when light was emitted. (It is 13.8 billion years old today.)

Redshifts can be easy to estimate for galaxies. However, the physics of quasars makes redshift determination a bit harder. In this dataset, we only include those quasars whose redshifts were determined by "visual inspection." Visual inspection is laborious: it would be nice to see if we can learn a statistical model that takes in the quasar's brightness at various wavelengths and precisely predicts the redshift.

Anyway, that's your goal.

One quirk here is that the dataset you are working with combines brightness information from SDSS with brightness information from *GALEX*, the *Galaxy Evolution Explorer*, an orbiting satellite that made observations in the *ultraviolet* band of the electromagnetic spectrum between 2003 and 2012. By adding this information, one can presumably do a better job predicting redshifts than one would do with optical-band SDSS data alone.

The dataset in this directory contains a response variable (`redshift`) along with 10 predictor variables:

| variable name | description |
| ------------- | ----------- |
| `ra`,`dec` | right ascension, declination (celestial longitude and latitude) |
| `(u,g,r,i,z)mag` | quasar magnitude in the u, g, r, i, and z bands of the optical and near-infrared |
| `nmag` | quasar magnitude in the ultraviolet n band |
| `gal_abs_u`,`log_nh_gal` | two measurements relating to dust and gas content along the line of sight |

A question you might have immediately is "what is magnitude?" The magnitude is a logarithmic measure of an object's brightness, where (a) a difference of five means a factor of 100 in brightness, (b) the brightest stars in the night sky have a magnitude of approximately zero, and (c) higher numbers means the objects are *fainter*(!). Thus a magnitude of 20 means an object is some 100 million times fainter than, say, Sirius.

Note that multicollinearity will be an issue here: a high g-band magnitude will tend to be associated with a high i-band magnitude, etc. In order to perform effective inference with these data, you would want to consider mapping the magnitudes to *colors*, which are differences in magnitude for adjacent bands: n-u, u-g, g-r, r-i, i-z. This will effectively mitigate some or all of the dataset's multicollinearity, but...you might pay a price with reduced predictive ability. If you do make the transformation to colors, you should at least check to see if the untransformed data give better predictions.

Onwards!
