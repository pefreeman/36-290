
Predicting Galaxy Masses and Star-Formation Rates from Emission-Line Equivalent Widths

[NEW in Fall 2018]

Galaxies are collections of stars and gas that give off light in all regimes
of the electromagnetic spectrum. One technique to zoom in and see how much
light is given off at specific wavelengths is optical spectroscopy. 

In this project, you'll work with data collected by the spectrograph of the 
Sloan Digital Sky Survey (or SDSS). Canonical examples of SDSS spectra are
given in panels 24 through 29 on

http://classic.sdss.org/dr5/algorithms/spectemplates/

If you look at these spectra, you'll notice that they can be decomposed into
two components: a relatively smoothly varying component, dubbed the continuum,
and narrow troughs and spikes. The narrow troughs and spikes are specific
absorption and emission lines caused by transitions of electrons within atoms.
One specific line that is often seen strongly in emission is called "H alpha"
and it occurs at 656.3 nanometers (or 6563 Angstroms). H alpha is the primary
emission line of the so-called Balmer series, and it is caused when an
electron that is in the third quantum level of a hydrogen atom fall to the
second quantum level. Such action occurs when there is hot gas present in 
the galaxy (and thus perhaps star formation going on). 

Your dataset includes measurements of H alpha and nine other emission lines in
each of 21,046 galaxies drawn from the MPA-JHU catalog:

https://www.sdss.org/dr14/data_access/value-added-catalogs/?vac_id=mpa-jhu-stellar-masses

By "measurements," I specifically mean estimates of <i>equivalent width</i>,
which is one of those strange astronomy-specific quantities which you will
run across from time to time. You can look it up, but it suffices to say two
things: (1) equivalent width is defined so as to be a relative quantity, 
specifically the strength of a line relative to the amplitude of the 
continuum around it, so that two identical galaxies at different distances
from the Earth will have lines with the same equivalent widths; and (2)
larger equivalent widths are strong lines (taller spikes).

The equivalent widths are the predictor variables. As for the response
variable, there are two available: galaxy mass and galaxy star-formation rate.
The idea would be to work with the mass first, and if there is sufficient
time, work with the SFR; a sufficiently advanced student wielding sufficiently
advanced tools could try dealing with both at once as a multivariate response.
Galaxy masses and SFRs are usually estimated by fitting templates like the
ones linked to above to the galaxy spectra, and seeing which templates
yield, e.g., the smallest residual sum of squares. (Astronomers understand
this as "minimizing chi-square," which statisticians in turn understand as 
maximizing a Gaussian likelihood function.) In theory, the masses and the
SFRs should be related to the equivalent widths, but the devil is in the
details: can you construct a statistical model that does a good job of
predicting, e.g., mass while also being interpretable, by, e.g., telling
us which lines are the important ones for predicting mass?

