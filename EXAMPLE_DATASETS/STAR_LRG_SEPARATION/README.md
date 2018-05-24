Star-Luminous Red Galaxy Separation Using eBOSS+WISE Data

[Used in 36-198 in Spring 2016.]

The dataset, contained in Star_LRG_eBOSS_WISE.Rdata, consists of measurements 
of 45,664 objects observed by the Extended Baryon Oscillation Spectroscopic 
Survey (eBOSS), a part of the third phase of the Sloan Digital Sky Survey 
(SDSS-III). The objects are either stars in the Milky Way, or luminous red 
galaxies (LRGs). The issue is that stars and LRGs sometimes occupy the same
volumes of predictor space...can we use statistical modeling to predict when
an object is a star or an LRG, for instance?

The dataset consists of two variables, predictors and response. The
predictors for each object are

| Variable        | Description                                                 |
| --------------- | ----------------------------------------------------------- |
| mag.{U,G,R,I,Z} | The magnitude of the object in various SDSS bandpasses; see  https://en.wikipedia.org/wiki/Photometric_system for more precise information. Basically, our eyes perceive light from about 350 nm to 700 nm, and thus these bandpasses  collect light from the near-ultraviolet through the optical regime to the near-infrared. Higher magnitudes mean dimmer objects, and it is a logarithmic scale: a change in magnitude of 5 corresponds to a factor of 100 in brightness. |
| mag.{W1,W2}     | The magnitude of the object in two WISE bandpasses. WISE is an infrared all-sky survey instrument; W1 is at 3400 nm  and W2 is at 4600 nm. |

The response variable is the spectroscopic redshift of the object, where the
redshift, z, is defined as

lambda.observed = lambda.emitted*(1+z) .

lambda.emitted is the wavelength of a photon when it leaves the
galaxy, and lambda.observed is the wavelength of the same photon when we
observe it. Because the Universe is expanding, the wavelengths of photons
expand while they travel towards up. The redshifts range from ~0 (meaning,
by us, meaning, in the Milky Way, meaning, stars) to ~2 (meaning, far away, 
meaning, galaxies). A redshift of 2 means that the photons travel for 
~10 billion years between emission and observation. (Even a redshift of 
0.01 means photons travel for some 100 million years before observation!)

If you histogram the redshift, you will observe bimodality. All objects with 
redshift < 0.01 are actually stars and not galaxies, with very high 
probability. Thus you can turn the continuous response into a factor 
variable: 0 for stars, and 1 for galaxies. Your job, then, is to see if 
you can learn a classifier that can predict whether a newly observed 
unlabeled object (i.e., a newly observed object for which we have all
predictor measurements but not the redshift) is a star or galaxy.

(Note: you may also pursue this as a regression exercise, by leaving
the response variable alone. Or look down to the bottom of this file for
another possibility.)

One hint: it *may* be beneficial to work with colors and not magnitudes.
(I'm not saying it is. All I'm saying is that this is a data transformation
worth exploring.) To derive the colors, take the difference of magnitudes 
in two adjacent bandpasses, e.g., color.ug = mag.u - mag.g. The order, 
again, is u, g, r, i, z, W1, W2. (There is no need to derive other colors, 
like color.ur = mag.u - mag.r, because color.ur = color.ug + color.gr. In 
other words, given just the colors derived using magnitudes in adjacent 
bandpasses, you can compute any other color directly.) Why colors, 
you ask? Two identical galaxies at different distances from the Earth 
will have different magnitudes, but the same colors.

A second hint: astronomers working with colors often find it is beneficial
to include one of the magnitudes in the model. In other words, perhaps
working with six colors and, say, mag.i might yield better results than working
with just six colors alone. You should explore this.

And last: if you really want to go hog wild, you could perhaps create a model
that classifies an object as a star or galaxy, and *if* it is a galaxy, 
predicts the redshift.

