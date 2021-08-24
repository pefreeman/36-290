**Classification of Blazars in Fermi Gamma-Ray Data**

The [Fermi Gamma-ray Space Telescope](https://fermi.gsfc.nasa.gov/) is designed to detect the high-energy radiation emitted by exotic astronomical objects like active galaxies, galaxies that contain supermassive black holes at their centers. As matter spirals into these black holes, it emits copious amounts of radiation...so much so that sometimes, the small region immediately around the black holes is as bright or brighter than the rest of the galaxy. Beamed jets of matter can also stream away from the black holes (such as illustrated by the third figure on [this web page](https://fermi.gsfc.nasa.gov/fermi10/fridays/03022018.html).

We fixate on jets in particular because they are associated with a particular type of gamma-ray-emitting object, [BL Lacertae objects](https://en.wikipedia.org/wiki/BL_Lacertae_object) or BL Lacs. BL Lacs are objects where we are looking down the jets, i.e., the jets are pointed (nearly) directly at us. BL Lacs are historically hard to identify because their spectra, i.e., their light as dispersed by a prism, show few if any diagnostic features...for all we know, a BL Lac which is far from our Milky Way could simply be a variable star within our Milky Way.

The dataset in this directory has been derived from the [Fermi LAT 10-Year Point Source Catalog (4FGL)](https://heasarc.gsfc.nasa.gov/W3Browse/fermi/fermilpsc.html). To decompose the name of the catalog a bit: the LAT, or Large Area Telescope, is one of the two instruments onboard the Fermi satellite, while the term "point source" denotes any astronomical object that appears to have no physical extent (like a star...the photons seem to emanate from a point, at least from our point of view). The (processed) catalog contains 4263 point sources, of which 1226 are BL Lacs and, for our purposes, 3037 are "not BL Lacs." (These not-BL Lacs include other types of active galaxies, quasars, pulsars, and the dreaded "unknowns.") Your research goal is to identify the labeled BL Lacs in the data sample (as identified in the column `source_type`), given values for 20 predictor variables:

| variable name | description |
| ------------- | ----------- |
| `ra`,`dec` | celestial longitude and latitude |
| `flux_1_100_gev` | the photon flux (think: object brightness) for 1 - 100 gigaelectron-volts (a measure of photon energy) |
| `detection_significance` | a measure of the strength of the object's signal |
| `spectrum_type` | the type of dispersed photon model used to model the spectrum |
| `pivot_energy` | "the energy...at which the error in the differential photon flux in minimal" |
| `energy_flux` | the energy flux (brightness again) for 0.1 - 100 gigaelectron-volts, from the model spectrum |
| `***_flux_density` | "the differential flux at pivot_energy" for different spectral models (`pl`,`lp`,`plec`) |
| `***_index`,`***_beta`,`***_exp_factor`,`***_curve_significance` | various spectral model parameters |
| `npred` | the predicted number of photons observed from the source during the observation |
| `variability index` | the higher the number, the more variable the brightness over time |
| `frac_variability` | another metric of source brightness variability |

The paper that accompanies this catalog is that of [Ajello et al. (2020)](https://arxiv.org/pdf/1905.10771.pdf).

Note that the spectral models and variables associated with high-energy astronomer are often quite inscrutable to the non-astronomer. *Do not worry about understanding what each of the predictor variables represents!* (Leave that to the astrophysicists.) The important things to focus on are (a) can you effective classify BL Lacs, and (b) can you determine which of the predictor variables are most important for classification? (Variables that, in real life, you'd simply report by name to your astrophysicist client.)

Having said that: are there particular issues to look out for here? Why, yes. For instance, many of the predictor variables are highly skew, so you'd want to explore data transformations. Also, as these are observational data, they are, not suprisingly, going to be afflicted by multicollinearity. You'll have to determine whether useful inference is possible here...or does it come at the expense of (statistical) model predictive ability?

