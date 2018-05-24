
Modeling Galaxy Mass as a Function of Morphology Statistics

[Used in 36-198 in Spring 2017.]

The event which we dub the "Big Bang" occurred some 13.8 billion years ago. In
the immediate aftermath, the Universe was filled with hot plasma, a soup of
protons and electrons that persisted for some 380,000 years until temperatures
fell sufficiently for atoms to form. At this point, atoms (hydrogen and 
helium) were *almost* uniformly distributed in space...but there were regions
that were very slightly denser than average. These slight overdensities were
sufficient to allow the creation of all the structures we see today: stars,
galaxies, galaxy clusters and filaments and walls.

As you might guess, the galaxies evolve over time. You can intuitively think of 
a galaxy's life cycle as being born with spiral structure, accreting gas and 
merging with other spirals, and eventually being part of a large, gas-less 
elliptical galaxy. (See, e.g., 

http://cdn.spacetelescope.org/archives/images/screen/heic9902o.jpg

for canonical examples of ellipticals and spirals.) So at any given time in
the Universe's history, galaxies have an ensemble of appearances that is
different from the appearances of past or future ensembles. Via theory, 
astrophysicists can predict ensemble appearance, although there are many
free parameters in theoretical models that need to be statistically inferred
via observations of real galaxies.

How would one compare theoretical models and real galaxies, you might ask?
Well, given a particular theoretical model, one can in principal generate an
ensemble of simulated galaxies. So the question becomes: how do we compare 
real and simulated galaxies? This is difficult to do because galaxy images
are intrinsically high-dimensional objects; if we have, say, 1000 galaxy
images, each 100 x 100 pixels, then the ensemble of galaxies is 1000 points
in a 10,000-dimensional space. The so-called "curse of dimensionality," which
states that the amount of data needed to attain a particular level of
precision in statistical inference rises *exponentially* with the number of
dimensions, indicates that we won't be able to accomplish much with these
data.

So now what? One option is to reduce the dimensionality of the problem via
summary statistics. The canonical example of a summary statistic is the sample
mean, by which one replaces the information present in n data with a single
summarizing number. Astrophysicists (and we here at CMU) have, through the
years, defined a number of summary statistics that we apply to every galaxy
image, reducing the dimensionality of the data from > 1000 to ~10.

I've written a whole bunch of words, but haven't said yet what you are going
to do within the context of this problem. But now I will.

I have, in my possession, data from the Illustris project. See

www.illustris-project.org

and Vogelsberger et al. (2014; MNRAS, 444, 1518) for information about it. 
In short, Illustris was a massive hydrodynamical simulation that produced 
thousands of galaxies, traced through time. Greg Snyder of the Space 
Telescope Science Institute in Baltimore took these galaxies and created 
images of them, such as they would be seen by the Hubble Space Telescope
(Snyder et al. 2015; MNRAS, 454, 1886). I then took the images and ran them 
through my own software to derive seven summary statistics for each image, 
denoted (M,I,D,Gini,M20,C,A). (Don't worry about the definitions of each 
for now. For now they are just numbers. And to keep things simpler at the 
start, we will only concentrate on the last four statistics.) I thus have 
vectors of statistics for galaxies computed at a number of redshifts (where 
the redshift is a proxy for how far back in time we are observing the 
galaxies). To start with, we'll look at redshifts 1.5 (younger galaxies, 
existing earlier in time) and 1.0 (older galaxies, existing later in time).
(Note that we live at redshift 0.)

The question for you: can you statistically learn a model that relates the
summary statistics for simulated galaxies to their masses? 

The place to start is multiple linear regression. Read Chapter 3 of 
Introduction to Statistical Learning, and in particular read through the
lab exercises in the back of that chapter. Then run the code

mass_stats.Rmd

that is included in this directory. When the code has finished running, you
will have a matrix of predictors with four columns (Gini,M20,C,A)
and a vector of responses (log10(galaxy masses), in units of solar masses).
You can then run multiple linear regression

&gt; out = lm(response~.,data=predictors)

and interpret the results. (Note that I'm assuming you've installed R Studio.)

Where we go next depends on what results we get. Things that one could do
include best subset selection, regression trees, random forest regression,
and support vector machine regression. How far we get is up to you.

