
Predicting Galaxy Stellar Mass from its Photometry and Redshift

---

The dataset in this directory is from the Large Synoptic Survey Telescope (LSST) Data Challenge 1 (DC1). The name "Buzzard" in the dataset file names denotes the fact that these data were produced from the Buzzard simulation. (Simulated datasets are good because they allow astronomers to develop analysis tools ahead of when real data arrive...and they are good because true values for the response variables are known!) The variables for each of the 111,172 galaxies are the following:

| Variable | Description |
| -------- | ----------- |
| u | Galaxy magnitude in LSST u band (320.5-393.5 nm) |
| g | Galaxy magnitude in LSST g band (401.5-551.9 nm) |
| r | Galaxy magnitude in LSST r band (552.0-691.0 nm) |
| i | Galaxy magnitude in LSST i band (691.0-818.0 nm) |
| z | Galaxy magnitude in LSST z band (818.0-923.5 nm) |
| y | Galaxy magnitude in LSST y band (923.8-1084.5 nm) |
| u.err | Uncertainty for u-band magnitude |
| g.err | Uncertainty for g-band magnitude |
| r.err | Uncertainty for r-band magnitude |
| i.err | Uncertainty for i-band magnitude |
| z.err | Uncertainty for z-band magnitude |
| y.err | Uncertainty for y-band magnitude |
| log.mass | Galaxy stellar mass (log-base-10 solar masses) |
| redshift | Galaxy redshift |

In class you have learned what magnitude is (it's a logarithmic measure of brightness), and what redshift is (it's a directly observable proxy for a galaxy's distance).

Mass (and in particular stellar mass, not including gas and dust) is the most important intrinsic property of galaxies to estimate. Mass estimation is commonly done by using prior knowledge of physics: if we can generate a library (or dictionary) of galaxy brightness estimates as a function of wavelength (known as galaxy templates), we can compare each an observed galaxy and try to find the closest match. There are a whole host of issues with this which we won't get into. It suffices to say we will try something different...we will see if we can statistically learn a model relating photometry to mass.

I envision three separate exercises here. Not all exercises have to be completed for full credit, but completing them would make for the best overall story.

1. Relate photometry to mass without redshift.

2. Relate photometry to redshift, predict the redshifts, then relate photometry + predicted redshift to mass.

3. Relate photometry + redshift to mass.

The first exercise is only important in so much as to help answer the question of "how much does redshift information help mass estimation?" The second exercise is the most realistic, in so far as this is what an astronomer would probably do if he or she was not trying to estimate mass and redshift jointly with templates. The third exercise basically answers the question "if we have spectroscopic redshifts for all galaxies and thus don't have to estimate redshift, how will we do?"

Go forth and analyze!

