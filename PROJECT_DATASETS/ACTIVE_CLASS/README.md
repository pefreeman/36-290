**Classification of Active Galaxies Observed by SDSS**

The [Sloan Digital Sky Survey](https://www.sdss.org/) is the largest survey of the observable Universe to date. Carried out from the Apache Point telescope in New Mexico, SDSS has cataloged some 470 *million* different objects, including over 200 million galaxies outside our Milky Way. Normally, galaxy data consists of an image, as well as measures of brightness collected in five different bandpasses (dubbed *u*, *g*, *r*, *i*, and *z*) that span the optical regime of the electromagnetic spectrum. But for a subset of nearly three million galaxies, we also have high-resolution *spectra*. One may think of an astronomical spectum as what we get when we pass light through a prism: light is spread out, with low-wavelength photons being routed to a different part of the light collector than high-wavelength photons. Thus instead of five coarse measures of brightness, we end up with over 3,000! (See [this web page](http://classic.sdss.org/dr5/algorithms/spectemplates/), particularly plots 24-29, for examples of galaxy spectra collected by SDSS.) 

A spectrum shows the underlying physics at play in a galaxy. For instance, if a galaxy is *active*, i.e., if it is forming stars at an enhanced rate, or if it has a supermassive black hole at its center swallowing stars and gas and dust at a fast rate, then the spectrum will exhibit "spikes," or *emission lines*. (Look at, e.g., plot 27 of the spectral examples linked to above.) Astrophysicists can use these lines to infer what is going on in a galaxy, and to infer broadly whether the galaxy is star-forming or whether it has an active nucleus. That's what you are going to try to do with the data provided here...you will attempt to classify galaxies as either *STARFORM* or *AGN*, given features extracted from their spectra.

The dataset in this directory contains information for 28,820 galaxies that have been labeled (through other means) as being star-forming galaxies or galaxies with active nuclei. There are nine predictor variables:

| variable name | description |
| ------------- | ----------- |
| `z` | galaxy redshift (see below) |
| `O3_Hb` | the relative strength of the [O III] emission line |
|         | at 500.7 nanometers and the H beta line at 486.1 nm |
| `O2_Hb` | same as above, but for the [O II] lines at 372.6 and 372.9 nm |
| `sigma_o3` | the width of the [O III] line |
| `sigma_star` | the standard deviation of star velocities in the galaxy |
| `u_g`,`g_r`,`r_i`,`i_z` | the four colors of the galaxy (see below) |

First: what is *redshift*?

The short story is that the Universe is expanding, and photons traveling through it have wavelengths that are tied to the expansion. Since the Universe expands appreciably during the perhaps billions of years it takes photons to reach us from an object, the wavelengths of these photons also increase appreciably, making the objects appear redder (hence "redshift"). Redshift is simply the ratio of the observed wavelength of a photon from an object to its wavelength when it was emitted, minus 1. Thus objects in the local Universe have redshift near zero.

Second: what are *colors*?

Above, we stated that `u`, `g`, etc., were measures of brightness. To be more concrete, they are logarithmic measures of brightness, dubbed *magnitudes*, where (a) a difference of five magnitudes corresponds to a factor of 100 in brightness, (b) magnitudes near zero correspond to the brightest stars in the night sky, and (c) galaxies with higher magnitudes are *fainter*. Because magnitudes are highly correlated with each other and with galaxy distance, astronomers will often work with colors, which are simply differences in magnitude. Colors tend to be both less correlated with each other and less correlated with distance. (Any correlation with distance implies that the physics of galaxies change with time, i.e., that galaxies evolve.)

Third, and last: what are [O III], [O II], and H beta, and what is up with the square brackets?

O III is an emission line observed to be associated with oxygen atoms that are two electrons short of a full set of electrons. (The oxygen is thus *ionized*, as it might be in a high-temperature environment.) O II is similar, but the atoms are only one electron short. The square brackets are a historical anomaly: they indicate that the observed emission lines are "forbidden," meaning they occur in low-density gases and are not observed in typical Earth laboratory conditions. Finally, H beta symbolizes the second line of the hydrogen Balmer series: the line is formed by emission from atoms where electrons fall from the fourth energy level to the second one. (Lines involving the first energy level appear in the ultraviolet and are not seen in the spectra of the galaxies in this dataset. That's the Lyman series, by the way.)

So, where do you start?

As is usual, you start with exploratory data analysis (EDA) and perhaps with principal components analysis. However, if you are wondering where you would start in statistical learning, you'd start in the usual place--logistic regression--and work your way from there. Note that the classes are slightly unbalanced, so you'll want to take care in how you map your regression results to predicted classes.

Onwards!

