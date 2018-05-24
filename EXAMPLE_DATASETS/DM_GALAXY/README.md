
Predicting Galaxy Properties Given Those of Their Dark Matter Halos

[Used in 36-198 in Spring 2018.]

Let's start off by explaining what dark matter is. The Universe is composed 
primarily of three constituents: baryonic matter (the normal stuff we see
around us), dark energy, and dark matter. Dark energy is an unknown "substance"
that acts as a form of anti-gravity, and is causing the expansion of the 
Universe to accelerate. Dark energy does not concern us here, at least not
directly. Dark matter is something completely different from dark energy: it
is a substance (probably a yet-to-be-discovered particle) that has mass but 
cannot be seen: it only interacts gravitationally. The evidence is strong that 
it exists...we just don't know what it is. Dark matter tends to cluster in
so-called halos, inside of which baryonic matter clusters into galaxies.
(Note: there can be halos within bigger halos...the halos can overlap and
are thus do not necessarily operate independently.)

Next, let's talk about making inferences about the Universe. We are in the
era of "precision cosmology," wherein the leading model for Universe's 
evolution is the so-called Lambda CDM Big Bang theory. Lambda = it has dark
energy. CDM = cold dark matter (the dark matter moves slowly, not quickly).
Big Bang = the Universe began as a near singularity and has been expanding 
for the last 13.8 billion years. (The Big Bang theory does *not* explain what
the bang itself was; it is only concerned with evolution from a certain 
timepoint on forward.) The Lambda CDM theory has certain free parameters
(like the proportion of dark matter and the current rate of the Universe's
expansion, etc.). We try to infer those parameters by creating massive
simulations of the Universe and comparing their output with observations.
The simulations take CPU months on thousands of cores. They cannot be run
every day.

There are two main types of simulations: hydrodynamic simulations that include
baryonic matter and dark matter, and dark-matter-only (or DMO) simulations.
The former are computationally *very expensive* and thus we can only simulate 
small volumes. The latter are (in relative terms) much easier to generate.
But the latter have no baryonic matter, so they have no galaxies. If we want
to learn about the formation and evolution of galaxies (aside from the
evolution of the Universe as a whole), it's kinda nice to have galaxies.

So: can we use the results of hydrodynamic simulations to "paint" galaxies
into DMO simulations? From a statistical learning point of view: can we learn 
a relationship between the properties dark matter halos and the properties
of galaxies in a hydrodynamic simulation and use that relationship to 
predict galaxy properties for a given halo in a DMO simulation?

The data:

The data for this project, provided by Francois Lanuesse of CMU's 
McWilliams Center for Cosmology, comes from MassiveBlack-II, a 
high-resolution hydrodynamical simulation of the Universe's evolution 
with a volume of approximately one million megaparsecs cubed 
(Khandai et al. 2015; MNRAS, 450, 1349). Within this volume are 
dark-matter halos (overdense regions of dark matter), which in 
turn contain subhalos; within the subhalos are galaxies.

Each subhalo contains dark matter "particles," the entities which are 
tracked during the simulation.

The file Massive_Black_II.Rdata contains training data for
251,068 halos/galaxies, and test data for 123,661 halos/galaxies.

To load these data into R Studio, do the following (once you've set the working
directory to the one in which the data reside):

&gt; load("Massive_Black_II.Rdata")  
&gt; objects()  
[1] "pred.test"    "pred.train"   "resp.test.df"   "resp.train.df"

pred.test and pred.train are data frames that contain the following columns:

| Name | Description |
| ---- | ----------- |
| halos.vdisp | the velocity dispersion for the halos, i.e., the standard deviation of the velocities of their constituent particles |
| halos.vcirc | maximum circular velocities for the halos, which you can think of as "how fast the halos spin" |
| halos.rcirc | the distance from the center of the halo where the maximum circular velocity is achieved |
| halos.m_dm | the dark matter mass |
| r_parent | the distance from the halo to the center of its parent halo |
| shapesDM.q3d | the halos may be thought of as ellipsoids with axes a, b, and c. This variable is b/a. |
| shapesDM.s3d | this is c/a |
| thetaTid | misalignment angle of halo (details not important here) |
| phiTid | similar to thetaTid |

resp.test.df and resp.train.df are data frames that contain three different
response variables (to be clear: we will look at each response variable in
turn, and not all at once):

| Name | Description |
| ---- | ----------- |
| halos.m_star | stellar mass of galaxy in the halo |
| prop.sfr     | star-formation rate within the halo |
| prop.btr     | the bulge-to-total size ratio of the galaxy (0 = a flat disk, 1 = a 3D ellipsoid with no disk, in between = a mix) |

For instance, you could start your overall analysis by trying to do 
multiple linear regression (after doing exploratory data analysis, of course):

&gt; resp.train       = resp.train.df$halos.m_star  
&gt; resp.test        = resp.test.df$halos.m_star  
&gt; pred.train.small = pred.train[,1:5]  # first five columns  
&gt; pred.test.small  = pred.test[,1:5]   
&gt; lm.out           = lm(resp.train~.,data=pred.train.small)  
&gt; resp.test.hat    = predict(lm.out,newdata=pred.test.small)  
&gt; mse              = mean((resp.test-resp.test.pred)^2)

The last line defines the mean-squared error: this is the metric you will use
to determine the quality of fit of different models, and determine which 
model(s) fit(s) best.

