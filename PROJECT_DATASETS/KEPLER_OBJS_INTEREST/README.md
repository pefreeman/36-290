
Exoplanets, or extrasolar planets, are planets that exist outside of our
Solar System. Due to their small size and their faintness, it is almost
impossible to discover them via direct imaging; rather, they are discovered
indirectly, most commonly via

- the radial velocity method, in which one detects a star's (relatively tiny) 
wobble around its planetary system's center of mass; and
- the transit method, in which one detects an exoplanet passing in front of,
and thus partially eclipsing, its host star.

The transit method relies on a bit of luck: an exoplanet has to pass directly
between us and the host star. That sort of chance alignment is rare. Hence
for the transit method to be truly useful, we have to monitor *many* star
systems.

Between 2009 and 2013, NASA's *Kepler* satellite stared at a star field in
the constellation Cygnus and kept tabs on over 100,000 stars at once. 
Data processing software used to analyze all the light curves (i.e., the
brightnesses of each star as a function of time) identified "objects of
interest," i.e., stars with possible exoplanets.
The *Kepler* observations, along with observations made independently,
were used to take these objects of interest and classify them as
CONFIRMED (really an exoplanet), CANDIDATE (still not sure), or
FALSE POSITIVE (not really an exoplanet). 

The dataset in this directory contains 
18 measurements for each of 9177 KOIs (or *Kepler* Objects of Interest). 
The measurements fall into four general groups:

| type | variables (all preceded with "koi_") |
| ---- | --------- |
| exoplanet orbit-related | period, eccen, sma, incl, dor |
| transit/eclipse-related | impact, duration, depth |
| exoplanet property-related | ror, prad, teq, insol |
| host star property-related | srho, steff, slogg, smet, srad, smass |

The definition of each measurement is given 
[on this web page](https://exoplanetarchive.ipac.caltech.edu/docs/API_kepcandidate_columns.html).

Research question: can you train a classifier that can effectively 
differentiate between CONFIRMED and FALSE POSITIVE exoplanetary candidates?
Once you have done this, apply your model to the CANDIDATE data to inform
NASA which candidates are most worthy of followup, independent observations.

