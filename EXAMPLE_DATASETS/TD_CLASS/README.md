
Classifying Periodic Variable Objects Using Catalina Sky Survey Data

---

[Used in 36-198 in Fall 2016.]

This is a fairly "straightforward" project that offers an opportunity for the
exploration of statistical learning methods.

There are two types of objects in the sky: those whose luminosities vary over
time, and those whose luminosities don't vary over time. (This is a bit of a
lie...even the Sun's luminosity varies...but the variations for the second
class of objects are so small as to be essentially unobservable on human
timescales.) We can then take those objects whose luminosities vary, and split
them into two classes: those exhibiting periodic variations, and those 
exhibiting stochastic, or random, variations. Cepheid variables are an 
example of the first class, and quasars are an example of the second class.

The large-scale context for why we care about variability is the following.

The Large Synoptic Survey Telescope (LSST), situated in Chile, will observe 
the sky above the Southern Hemisphere for ten years, beginning in 2019 or so.
Every spot in the southern sky will be observed roughly 1,000 times. This
means that for every star or galaxy that LSST can observe, there will be
a time series of estimated apparent magnitudes (think luminosities). LSST 
will be the first telescope to observe many of these stars and galaxies,
and thus it will discover many variable objects. But astronomers don't want
to wait until the end of LSST's run to identify and study these objects...they
want identifications NOW. So, for instance, when LSST observes a portion of
the sky, software will attempt to quickly determine if there are objects in
that portion whose intensity has changed since the last observation. If the
software detects such objects, it will issue alerts to astronomers, since
perhaps these objects will disappear quickly and thus need to be observed
quickly by other telescopes. The number of alerts per hour for LSST is
expected to be 50,000.

Well, no robotic telescope program can follow up 50,000 LSST observations 
per hour.

So the current plan is to send the alerts to a so-called broker, which will
take the data and quickly try to determine how important it is to follow up
the LSST observation for any given object. Essentially the broker filters
the alerts.

What a broker could do is what you might do in this project: a broker might
look at the (possibly very short) time series of the current and past 
observations of the object, and attempt to classify it as being a particular
type of variable star or galaxy.

In this project, you will look at the time series data for known periodic
stars observed by the Catalina Real-time Transient Survey (CRTS). You can
read about the survey here:

http://nesssi.cacr.caltech.edu/CRTS/

but it suffices to say that the survey utilizes dedicated telescopes 
worldwide to monitor the northern and southern skies. Its (or one of its)
raison d'etre is to detect and characterize near-Earth asteroids, but we
will make use of the fact that while looking for asteroids, the survey found
many variable objects.

The Catalina Surveys Data Release 2 is here:

http://nesssi.cacr.caltech.edu/DataRelease/Varcat.html

---

One cannot generally work directly with the light curves (i.e., the time 
series of magnitudes) for each star, since the number of observations differs.
What one generally does is to extract features from the light curves. For
instance, if there are 66 magnitude measurements for a given star, we might
compute the sample mean (one feature), the sample standard deviation (another
feature), etc. 

From the Catalina Sky Survey data, I have extracted 17 features for 46,808
variable stars. The features are defined in Appendix A of 
Richards et al. (2011), which is
included in this directory. (Note that I did not extract all the features
that Richards et al. define.) The response variable (i.e., the data label)
is the variable type, numbered 1-17 and defined in Table 2 of Drake et al.
(2014) (also included in this directory). (Note that the counts for each
class does not necessarily equal the counts given in Table 2, especially 
for Class 4, RRab.)

To read the data into an <tt>R</tt> data frame, install the feather package 
and do:

&gt; library(feather)</br>
&gt; data = data.frame(read_feather("./css_data.feather"))

(If you are comfortable with tibbles, just use <tt>read_feather()</tt> 
directly. If you've no idea what tibbles are, stick with data frames for 
now and read Chapter 10 of Grolemund &amp; Wickham's <i>R for Data 
Science</i>, which is free online at <tt>r4ds.had.co.nz</tt>.)

(Another reason I provide the data in a feather file is that it can also
be loaded relatively easily into a <tt>Python</tt> analysis, 
via <tt>pandas</tt>.)

The predictor variables are in columns 1-17 and the variable type is in
column 18.

---

How to start? If you do

&gt; table(data$var.type)

you will discover that Class 1 (contact binaries) dominates the dataset. So
to keep things simple as you play with classification algorithms, perhaps
try to predict Class 1 vs. Classes 2-17. If you go that route, you should
do something like the following:

&gt; predictors = data[,1:17]</br>
&gt; response   = data[,18]</br>
&gt; response[response>1] = 0

Onwards to exploratory data analysis and then to, e.g., logistic regression 
and random forest.

