
Can a Galaxy's Appearance Inform Estimates of its Distance From Earth?

---

[Used in 36-495 in Fall 2017.]

The basic idea: in order to perform statistical inference on models that
describe the Universe, we need to know where exactly our observed data are,
i.e., we need to know how far away a galaxy that we observe is. We cannot
use a tape measure, obviously. One way to estimate galaxy distance is by
measuring its redshift, i.e., the amount by which the wavelength of light
emitted by the galaxy stretches while the light travels from the galaxy to us.
(Why does the wavelength change? Because it is linked to the underlying 
expansion of the Universe. If the Universe doubles in size while a photon
travels to us, its wavelength increases by a factor of two.)
Given a redshift and a model for the Universe (meaning, really,
parameter values for a Lambda-CDM Big Bang model), one can estimate a
physical distance to a galaxy.

Redshift is estimated by looking at dispersed spectra of galaxies and trying
to find sharp absorption or emission lines due to different atomic transitions.
If we have high-resolution spectra, then determining redshift is easy 
(assuming the spectrum has lines in the first place). However, for most 
galaxies, all we have are low-resolution spectra, and I do mean low: we have
what is called "photometry" for, e.g., five or six different wavelength
ranges.

One cannot look at the photometry of a single galaxy and determine the
redshift of that galaxy. However, one *can* throw the data of thousands of 
galaxies into an estimation algorithm and use the cumulative information
to predict redshifts for each galaxy. (This is assuming that we know the
labels, i.e., we know the redshifts, for some subset of the data.)
For simplicity, we are going to skip over the details of this. It suffices 
to say that out of such algorithms, one might get a regression estimate: 
given the photometry, we predict the mean of the probability density 
function for the redshift.

Now, many algorithms simply try to get point estimates given photometry.
But can the precision and accuracy of point estimates be improved by
including other information about the galaxies as well? That's the question
you will try to answer with this dataset.

---

To read in the data, do

&gt; load("photo_morph.Rdata")

This loads in two variables: response, a vector of redshifts of length 3419,
and predictors, a data frame containing galaxy measurements and statistics 
with 3419 rows and 16 columns. The predictors are the following:

| Name | Description |
| ---- | ----------- |
| mag.i | Logarithmic measure of brightness in i-band (wavelength 814 nm) |
| col.[Vi,iJ,JH] | Colors: differences of magnitudes (e.g., V-band magnitude - i-band magnitude) |
| [V,J,H].G | Morphology summary statistic: Gini coefficient in V, J, and H bands (606 nm, 1250 nm, 1600 nm) |
| [V,J,H].M20 | Morphology summary statistic: M20 statistic in V, J, and H bands (606 nm, 1250 nm, 1600 nm) |
| [V,J,H].C | Morphology summary statistic: concentration statistic in V, J, and H bands (606 nm, 1250 nm, 1600 nm) |
| [V,J,H].size | Morphology summary statistic: observed galaxy size in V, J, and H bands (606 nm, 1250 nm, 1600 nm) |

---

An idea of where to start:

1) Linear regression, applied to all non-morphological predictors (the first 
four), and then to all predictors.

2) Linear regression with subset selection, to explore the importance of 
predictors.

One would then move on to other algorithms. This problem lies at an
intersection between inference and machine learning: yes, the ultimate
goal is to predict redshift, so ML algorithms may be useful, <i>but</i>
we also want to learn whether certain predictors (and which ones!) are 
useful, so inferential approaches like subset selection and lasso may
also be useful. Can you come up with an analysis that gets the best of 
both worlds: predictive accuracy <i>and</i> interpretability?

