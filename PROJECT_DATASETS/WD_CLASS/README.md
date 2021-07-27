**Classification of White Dwarfs Observed by SDSS**

The [Sloan Digital Sky Survey](https://www.sdss.org/) is the largest survey of the observable Universe to date. Carried out from the Apache Point telescope in New Mexico, SDSS has cataloged some 470 *million* different objects, including over 250 million stars. Normally, stellar data consists of measures of brightness collected in five different bandpasses (dubbed *u*, *g*, *r*, *i*, and *z*) that span the optical regime of the electromagnetic spectrum. But for a subset of just over one million stars, we also have high-resolution *spectra*. One may think of an astronomical spectum as what we get when we pass light through a prism: light is spread out, with low-wavelength photons being routed to a different part of the light collector than high-wavelength photons. Thus instead of five coarse measures of brightness, we end up with over 3,000! (See [this web page](http://classic.sdss.org/dr5/algorithms/spectemplates/), particularly plots 21-22, for examples of spectra collected by SDSS.)

Some of the stars that SDSS has observed are actually not stars at all, at least in the way we normally think of stars. They are actually *white dwarfs*, which are what remain after stars end their lives by ceasing nuclear fusion in their cores and pushing their gaseous outer layers away. (A *planetary nebula* is a white dwarf in the making, when a star's gas is being pushed away.) A white dwarf is an Earth-sized body with a mass approximately that of the Sun, a body which would shrink more under gravity if it wasn't for the so-called degeneracy pressure of the electrons resisting further compaction. 

Not all the spectra of white dwarfs look the same. (See plots 21 and 22 again at the web page linked to above.) White dwarfs of spectral type A (or DA) have spikes in their spectra that are caused by electon transitions in hydrogen atoms. Other types are, e.g., B (or DB), C, O, Z, etc. Type A white dwarfs are the most common, comprising some 80% of all white dwarfs.

If you take the time to collect a spectrum and look at it, it is easy enough to classify a white dwarf. However, it is far easier (and faster) just to collect information like the `u`, `g`, `r`, `i`, and `z` *magnitudes*, as well as where the white dwarfs are in the sky, and how fast they are moving relative to background stars. Can we use just this information to determine spectral types?

"Wait...you said magnitudes." 

OK: above, we stated that `u`, `g`, etc., were measures of brightness. To be more concrete, they are logarithmic measures of brightness, dubbed magnitudes, where (a) a difference of five magnitudes corresponds to a factor of 100 in brightness, (b) magnitudes near zero correspond to the brightest stars in the night sky, and (c) stars with higher magnitudes are *fainter*. 

Now, back to what we were talking about: can we just use easily obtained, non-spectroscopic information to determine spectral types? That's what you will try to do in this project. The dataset in this directory contains information for 9,112 white dwarfs, labeled as being either `DA` (spectral type A) or `NOT DA`. There are eight predictor variables:

| variable name | description |
| ------------- | ----------- |
| `ra`,`dec` | celestial longitude and latitude |
| `umag`,`gmag`,`rmag`,`imag`,`zmag` | magnitude in each SDSS bandpass |
| `pm_tot` | proper motion (i.e., motion relative to background stars) |

So, where do you start?

As is usual, you start with exploratory data analysis (EDA) and perhaps with principal components analysis. However, if you are wondering where you would start in statistical learning, you'd start in the usual place--logistic regression--and work your way from there. Note that the classes are unbalanced, so you'll want to take care in how you map your regression results to predicted classes.

Onwards!

For more information on this catalog, see [this paper](https://arxiv.org/pdf/1411.4149.pdf).

