
Can We Detect the Morphology-Density Relationship in the COSMOS Field?

---

[Used in 36-198 in Fall 2016.]

Coarsely, galaxies come in three types: spirals, ellipticals, and irregulars (aka galaxies that *aren't* spirals or ellipticals). You can think of galaxy types and galaxy evolution this way: sufficiently massive galaxies are born as spirals, collide with other galaxies (leading to an irregular appearance, at least for some amount of time), and eventually become ellipticals. The probability of collisions that involve enough mass to turn a spiral into an elliptical increases if there are more galaxies in a given volume of space, thus we have the morphology-density relationship: more crowded regions of space feature a higher proportion of elliptical galaxies.

* OK...so what am I going to do?

You are going to see if you can learn a statistical model that relates summary statistics of the morphologies of galaxies in the COSMOS field to the local density of galaxies.

* Gah...where do I start?

By reading this.

First: what is morphology? As you probably gathered from above, it is a galaxy's appearance when projected onto the sky. Astronomers like to discretize morphology by grouping galaxies into classes, but this is not a good thing to do, statistically: discretization throws away information. In a perfect world, we would like to work with galaxy images directly, treating morphology as a continuous family of distributions. But that's too computationally intensive, at least at this time, since we'd be dealing with data that inhabit an N-dimensional space, where N is the number of image pixels. So we compromise: we generally compute summary statistics for galaxy images. Just like we might summarize a data sample of student heights with the mean, we summarize galaxy images with a number of statistics (for this project, we'll use G, M20, C, and A, which you don't need the definitions of, for now). Your initial data will have values for these four statistics for 739 galaxies observed in the i band (around 814 nm) in the COSMOS field. (For more than you ever wanted to know about the COSMOS field, see http://candels-collaboration.blogspot.com/2012/07/cosmos-cosmic-evolution-survey.html) The data were collected as part of the Hubble Space Telescope CANDELS program (Grogin et al. 2011 [ApJS, 197, 35], Koekemoer et al. 2011 [ApJS, 197, 36]).

Second: how do we define the density? To answer this, we need to know how far away our galaxies are. To determine distance, we estimate something called redshift, which is akin to a Doppler shift. It is caused by the fact that the Universe expands as the light from a galaxy travels to Earth, causing photon wavelengths to expand. The farther the galaxy, the more the wavelengths shift from what they were at the time of emission. Redshift is easy to estimate if there is an atomic line in a galaxy's spectrum: just see how much the line shifts:

z = lambda_obs / lambda_emit - 1

where lambda_emit is the true wavelength of the atomic transition, lambda_obs is the wavelength we observe the line at, and z is the redshift. If we don't have spectra, though, we have to use estimates based on a galaxy's photometry.  Photometry is essentially very low resolution spectroscopy; instead of measuring a galaxy's light in thousands of wavelength bins, we might have five bins. Photometric redshifts have large errors; for this project, the point estimates are the modes of the estimated probability densities for each of the galaxies. 

Once one has the redshifts, one can estimate the relative local density for each sample galaxy. I do this via a simple algorithm:

1. For a given value of z, count the sample galaxies between z and z+delta.z, where delta.z here is 0.05 (ad hoc choice).

2. Divide that number of galaxies by the total comoving volume between z and z+delta.z. To compute this volume, I start with equation 29 of Hogg (1999; arxiv.org/abs/astro-ph/9905116) and work backwards, assuming a flat Universe (Omega.k = 0) with a Hubble constant (H.o) of 70 kilometers per second per Megaparsec, Omega.M of 0.27, and Omega.Lambda of 0.73. The speed of light, c, is 299,792.458 kilometers per second. The comoving volume is thus in Megaparsecs^3.

3. Since all that matters is the relative density, I divide all my estimated 
densities by the maximum value, so all the densities are between 0 and 1.

To summarize...the data, available both in mdr.csv or mdr.Rdata:

| Name | Description |
|-----|-----|
| G | Gini coefficient (e.g., Lotz et al. 2004, ApJ, 128, 163) (predictor) |
| M20 | Moment of light statistic (e.g., Lotz et al., ibid.) (predictor) |
| C | Concentration of light statistic (e.g., Conselice 2003, ApJS, 147, 1) (predictor) |
| A | Asymmetry of light statistic (e.g., Conselice 2003, ibid.) (predictor) |
| z | Photometric or spectroscopic redshift |
| d | Estimated density of sample galaxies at z (response) |

