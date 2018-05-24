
Identifying Stars in the Draco Dwarf Spheroidal Galaxy

[Used in 36-198 in Spring 2016.]

The Milky Way galaxy is surrounded by a numerous number of small and faint
galaxies known as dwarf galaxies. One of them is the Draco Dwarf, a dwarf 
spheroidal galaxy lying in the constellation of Draco. Dwarf spheroidals like
the Draco Dwarf are thought to be dark-matter dominated: they contain 
relatively few stars and virtually no gas for making new stars, as they lost
gas and (some) stars in the past via interactions with larger galaxies like 
the Milky Way. Because of this, dwarf spheroidals are good targets for those
wishing to study dark matter and in particular the posited annihilation of
dark matter particles.

This project, however, is not about dark matter per se.

In order to study the properties of dark matter in the Draco Dwarf, one needs
objects that trace its presence, i.e., one needs to study the positions and
velocities of the stars that are interacting with the dark matter. (Dark matter
is dark, after all.) This means that we have to identify the stars that lie
in the Draco Dwarf. This is not as simple as it sounds: when we observe the
Draco Dwarf, we observe its stars as well as foreground stars that actually
lie in the Milky Way. Your initial job is to use techniques of unsupervised
learning to disambiguate stars of the Draco Dwarf from those of the Milky Way,
using observed star properties such as velocity relative to Earth, magnitude
(or brightness), metallicity (the proportion of elements heavier than helium),
etc. "Unsupervised learning" simply means that you have no ground truth here;
in supervised learning, you would learn a predictive model using, e.g., stars
that are known to be in Draco. However, we don't have the luxury of having such
definitive data here...

### Data

The data file draco_photometry.Rdata contains information on 2,778 observations
of TBD individual stars. You would input it into an R session like so:

&gt; load("draco_photometry.Rdata")

(This is assuming you have set your working directory to where the data lays.)
After loading this file, you would have the following 12 variables:

| Name | Description |
| ---- | ----------- |
| ra	|	right ascension (or celestial longitude), in degrees |
| dec	|	declination (or celestial latitude), in degrees |
| signal.noise|	the signal-to-noise of the star (larger value == brighter star) |
| velocity.los|	radial velocity, along the line-of-sight, in km/s |
| temperature|	the star's effective temperature (the Sun's is 5500 K) |
| log.g	|	the log of the surface gravity in cgs units |
| metallicity|	the proportion of elements heavier than helium in the star |
| mag.{ugriz}|	the star's apparent magnitude in the SDSS u-band, etc.; larger values indicate fainter stars |

### Initial Analyses

1. Exploratory Data Analysis (EDA). Make scatter plots of each variable against the others. Make histograms of each variable. 
2. In "An Introduction to Statistical Learning," read sections 10.3 and 10.5 and explore the use of K-means clustering and hierarchical clustering methods on the given data.

