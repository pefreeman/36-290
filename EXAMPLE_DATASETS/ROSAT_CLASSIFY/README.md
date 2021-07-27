**Classification of Point-Like X-ray Sources in the ROSAT 2RXS Survey**

The *ROSAT* X-ray telescope was launched in 1990, and over the course of the next decade it compiled observations of more than 150,000 objects. X-rays are energetic photons, and so the types of sources that *ROSAT* observed were not necessarily your everyday stars and galaxies. Instead, *ROSAT* observed so-called "X-ray binaries," binary systems that included compact stellar remnants (white dwarfs, neutron stars, black holes); emission from supermassive black holes at the centers of active galaxies and quasars; emission from the hot gas permeating galaxy clusters; etc. (The Sun gives off some X-rays too, but not enough to be detected in the X-ray band from far away by an alien civilization. It takes a source with lots of "power" to be seen across the galaxy or across the observable universe.)

Some X-ray sources are extended: the emission region is spread across a relatively wide area, like the expanding gas cloud of a supernova remnant, or the hot gas of a galaxy cluster. But many others are point-like, and are thus hard to classify. Stars look like points in the sky, but so do the active regions around supermassive black holes at the centers of galaxies. How do we tell the difference?

It helps to make follow-up observations of sources with telescopes that observe in different regimes of the electromagnetic spectrum. (The regimes, from highest-energy to lowest-energy, are gamma rays, X-rays, ultraviolet, optical, infrared, microwave, and radio.) In the dataset here, the X-ray measurements are augmented with brightness measurements from the optical regime (*Gaia* and the *Sloan Digital Sky Survey* [or *SDSS*]) and the infrared (the *Wide-field Infrared Survey Explorer* [or *WISE*]).

The dataset contains 26 predictor variables representing each of 4,198 separate astronomical objects:

| Variable Name | Definition |
| ------------- | ---------- |
| `RXS_ExiML` | detection likelihood (higher means "more sure about detection")|
| `RXS_CRate` | source X-ray count rate |
| `RXS_Ext`   | source extent in *ROSAT* CCD pixels |
| `RXS_LOGGALNH` | log-base-10 of hydrogen column density (cm<sup>-2</sup>) |
| `RXS_SRC_FLUX` | source flux in 0.1-2.4 keV band (erg/cm<sup>2</sup>/sec) |
| `ALLW_(W1,W2,W3,W4,J,H,K)mag` | source magnitudes as measured by WISE, in 7 infrared (IR) bands |
| `SDSS_MODELMAG_(u,g,r,i,z)` | first version of source magnitudes as measured by SDSS, in 5 optical and near-IR bands |
| `SDSS_FIBER2MAG_(u,g,r,i,z)` | second version of source magnitudes as measured by SDSS, in 5 optical and near-IR bands |
| `Z_BEST` | best estimate of source redshift |
| `GAIA_DR2_phot_(g,bp,rp)_mean_mag` | source magnitudes as measured by *Gaia*, in 3 optical bands |

Given what is stated in the table, some further definitions are in order.

First, the telescopes:

1. *RXS*: variables associated with *ROSAT* observations
2. *ALLW*: variables associated with *WISE*
3. *SDSS*: variables associated with *SDSS*
4. *GAIA*: variables associated with *Gaia*

Second, the terminology:

1. column density: imagine a square tube with cross-sectional area of one square centimeter that extends from the Earth to the source...the column density is the number of hydrogen atoms inside that tube...the more hydrogen atoms, the more X-rays from the source that get absorbed before getting to Earth
2. magnitude: a logarithmic measure of source brightness...an increase in magnitude of 5 is equivalent to a factor of 100 **reduction** in brightness...the brightest stars in the night sky have magnitude approximately zero
3. wavelength bands: `W1` and `u` and `rp`, etc., denote that the observation was made with a particular filter placed in the light beam of the telescope...for instance, the `g` filter only lets in light with wavelengths around 0.475 microns...see [this Wikipedia page](https://en.wikipedia.org/wiki/Photometric_system) for the effective wavelengths associated with each band
4. model vs. fiber2: magnitudes can be estimated via a variety of algorithms...these happen to be names for two of these algorithms
5. redshift: the ratio of the wavelength of a photon when it reaches Earth to when it was emitted, minus 1. Example: if a photon has wavelength 1 micron when emitted, and 3 microns when observed, the redshift is 3/1 - 1 = 2. A larger redshift means the object that emitted the photon is further away. Redshift is thus a directly observable proxy for the physical distance to an extragalactic object.

The response variable is categorical and the value is assigned through the visual inspection of images and data. *Can we do better with statistical learning?*

| Source Type | Number |
| ----------- | ------ |
| `QSO`         | 2,014 |
| `BLAGN`       | 1,419 |
| `GALAXY`      | 385 |
| `STAR`        | 243 |
| `NLAGN`       | 137 |

- `QSO`: a quasi-stellar object, or quasar. This is an object whose light 
comes primarily from the vicinity of a supermassive black hole at the center
of an otherwise normal galaxy. As material falls into the black hole, a massive
amount of light is emitted; the more material, the brighter the quasar.
If you reduce the amount of material, the quasar "turns off." The last quasars
turned off a long time ago, so the nearest quasars are far from Earth.
- `BLAGN`/`NLAGN`: broad-line and narrow-line active galactic nuclei (AGN).
AGN are fainter than quasars but there's still a lot of action in the very
center of the galaxy. Broad-line vs. narrow-line is a matter of the
observer's vantage point.
- `GALAXY`: a vanilla galaxy with not much going on at the center. The Milky
Way is a galaxy with a supermassive black hole in the center that presumably
acted like an AGN in the past.
- `STAR`: a ball of gas in the Milky Way. Stars are sample contaminants.

Coarse groupings would be `QSO` and `BLAGN` versus `GALAXY` and `NLAGN` versus `STAR`. So while there are many analyses one could carry out here, a first one would be to learn a classifier that differentiates between the first two of these coarse groups, while taking into account class imbalance. Alternatives would be to see how well one can differentiate between the `QSO` and `BLAGN` classes, or the `GALAXY` and `NLAGN` classes, etc., while again taking class imbalance into account.

The data model for this dataset is provided [here](https://data.sdss.org/datamodel/files/SPIDERS_ANALYSIS/VAC_spiders_2RXS_DR16.html), while
the most up-to-date reference for this dataset is [Comparat et al. (2020)](https://arxiv.org/pdf/1912.03068.pdf).

