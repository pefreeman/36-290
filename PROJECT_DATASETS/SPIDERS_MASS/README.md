**Predicting the Masses of Biggest Cluster Galaxies from their Optical Brightnesses and Shapes**

In the 13.8 billion years since the Big Bang, the Universe has gone from being filled with a very nearly uniform fog of hot gas (hydrogen and helium) to being very spatially sparse, with much matter tied up in the stars and gas and dust of galaxies like the Milky Way. The arrangement of galaxies is not spatially uniform; rather, the so-called "large-scale structure" of the Universe is something akin to a sponge, with holes (i.e., voids) and with connective strings (filaments) that come together at regions of enhanced galaxy density (clusters). To get the basic idea, see [this video](https://www.youtube.com/watch?v=eDGtFRj4xXc), or [this one](https://www.youtube.com/watch?v=74IsySs3RGU). For each video, keep in mind that a point in the simulation is for all intents and purposes a whole galaxy. It may also help to know that 1 Mpc (or 1 Megaparsec) is about 3.3 million light years across, or about 100 times the radius of the Milky Way. Thus the scales shown in these videos is incomprehensively vast. Large-scale structure, indeed.

Galaxy clusters, those areas of enhanced galaxy density at the intersection of filaments, are the largest gravitationally bound structures in the Universe. This means that galaxies in the cluster orbit the cluster's center of mass, albeit while being perturbed by the gravitational pull of all the other galaxies that are nearby. Over time, it generally becomes the case that galaxies merge and grow larger, and this is especially true near the centers of clusters, where one very large, very "fat" galaxy may form: the so-called "biggest cluster galaxy," or BCG.

Determining the properties of BCGs and how they affect their environments (and how they affect the appearances of farther-away galaxies seen behind them) is an important topic in astrophysics. A primary property to determine is mass: more massive objects distort spacetime more (according to General Relativity) and thus have more of an effect on their environments.

Now, before launching into the dataset itself, note that clusters have to be detected and that there are roughly four primary means of detecting them, including by detecting the X-rays emitted by the hot gas that envelops the cluster. One program for detecting clusters via X-ray observations, based at the Max Planck Institute for Extraterrestrial Physics in Germany, is dubbed "Spectroscopic Identification of eROSITA Sources," or, convienently, SPIDERS.

The data you will examine include brightness and shape information for 390 BCGs collected by the SPIDERS team. After data pre-processing, there are 66 predictor variables:

| Variable Name | Description |
| ------------- | ----------- |
| `CLUZSPEC` | Redshift of cluster (see below) |
| `RA_BCG`,`DEC_BCG` | Celestial longitude and latitude of the BCG |
| `GAL_sdss_(g,r,i)_(modS,modV,modSX)_CHI2NU` | Quality of spectral-fit metric of 9 separate combinations of wavelength band and model (see below) |
| `GAL_sdss_(g,r,i)_(modS,modV,modSX)_C1_MAG` | Model magnitude of BCG in specified wavelength band (see below) |
| `GAL_sdss_(g,r,i)_(modS,modV,modSX)_C1_RE` | Modeled radial extent (i.e., size) of BCG in specified wavelength band |
| `GAL_sdss_(g,r,i)_(modS,modV,modSX)_C1_N` | Best-fit shape model parameter of BCG in specified wavelength band (see below) |
| `GAL_sdss_(g,r,i)_(modS,modV,modSX)_C1_AR` | Best-fit axis ratio parameter of BCG in specified wavelength band (see below) |
| `GAL_sdss_(g,r,i)_(modS,modV,modSX)_C1_PA` | Best-fit position angle parameter of BCG in specified wavelength band (see below) |
| `GAL_sdss_(g,r,i)_modSX_C2_(MAG,RE,AR,PA)` | Similar to above, but for second model component in a multi-component fit |

Some further defintions:

1. Redshift: the ratio of the wavelength of a photon when it reaches Earth to when it was emitted, minus 1. Example: if a photon has wavelength 1 micron when emitted, and 3 microns when observed, the redshift is 3/1 - 1 = 2. A larger redshift means the object that emitted the photon is further away. Redshift is thus a directly observable proxy for the physical distance to a cluster.

2. Spectral-fit metric: how well a given model fit to a given set of data. The metric here is reduced chi-square. (Contact me for more detail on chi-square if you want it.) A smaller number is better, and the optimum value is approximately 1.
3. SDSS: indicates the observation of the BCG was done by the Sloan Digital Sky Survey. (Note: the measurements here are from followup observations by SDSS in the optical band of the electromagnetic spectrum, not from the X-ray observations used to detect the clusters in the first place.)
4. g,r,i: the g (0.475 micron), r (0.622 micron), and i (0.763 micron) bands. A BCG was thus observed by SDSS at at least three separate times, each time with a different filter in the light path that let in specific ranges of wavelengths of light and only those.
5. modS,modV,modSX: these indicate the model used. The light from the BCG was rebinned so as to create a radial profile (i.e., the differential amount of light emitted as a function of distance from the center of the BCG), and the observed profiles were fit with Sersic, de Vaucouleurs, and Sersic+exponential models. Model details can be dug up upon request.
6. MAG: magnitude, or logarithmic brightness, of the BCG. Lower values mean brighter objects. A difference of 5 magnitudes maps to a factor of 100 in brightness. The brightest stars in the night sky have magnitude approximately zero.
6. N: each of the models has a parameter which modifies the shape of the radial profile; that parameter here is N.
7. AR: the BCG, projected onto the sky, appears as an ellipse. The AR, or axis-ratio, is the ratio of the length of the semi-minor axis of the measured ellipse to the semi-major axis. The value must be between 0 (a line) and 1 (a circle).
8. PA: the ellipse mentioned above has an arbitrary rotation relative to a defined set of coordinate axes. The PA, or position angle, is thus just a measure of that arbitrary rotation. The value must be between 0 degrees and 180 degrees.

The response variable is log-base-10 of the stellar mass of the BCG, as measured in solar masses. Now, as we cannot put the BCGs on scales, we do not have ground truth here: the masses are themselves estimates made using physics codes that map template spectra (i.e., artificially created model spectra, which take mass as an input) to brightness information in the ultraviolet, optical, and infrared domains. 

*The question here is: can we effectively skip using computationally intensive codes by uncovering a direct relationship between the brightness and shapes of BCG in three optical bands and the BCG stellar mass?*

The data model for this dataset is provided [here](https://data.sdss.org/datamodel/files/SPIDERS_ANALYSIS/SpidersXclusterBCGs.html), while
the most up-to-date reference for this dataset is [Clerc et al. (2020)](https://arxiv.org/abs/2007.05484).
