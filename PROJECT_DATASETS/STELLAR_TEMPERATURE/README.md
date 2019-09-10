
*Gaia*, a space-based telescope commissioned by the European Space Agency, is performing an all-sky survey of objects in the Milky Way at optical wavelengths. As stated in Bai et al. (2019; Astronomical Journal, 158, 93), "[t]he main objective of the *Gaia* mission is to survey more than one billion stars in order to understand the structure, formation, and evolution of our Galaxy."

One of the properties we wish to estimate for stars are their temperatures. A typical star emits a blackbody spectrum with an effective temperature in the range 3,000 to 10,000 Kelvins. (Reminder: the Kelvin scale is the same as the Celcius scale, except 0 degrees Kelvin is absolute zero, or -273 degrees Celcius.) The Sun, for instance, emits a blackbody spectrum with effective temperature 5800 K.

In order to learn a statistical model to estimate effective temperature, the *Gaia* team used a training dataset consisting of 65,200 stars for which broad-band magnitudes were known along with the effective temperatures. Bai et al., concerned that the small size of the training dataset could lead to issues with the precision and accuracy of the *Gaia* team model, greatly expanded both the number of objects used for training their own model (3,810,143 stars) and the number of measurements taken for each star.

Your goal is to take the Bai et al. training dataset and use it to develop your own model of stellar effective temperature.

The dataset in this directory contains 24 measurements for each of 250,000 stars selected randomly from the original sample of 3,810,143 stars. (I selected a subset so as not to run afoul of GitHub storage limits. If you wish to have the full dataset, I can make that available.) The response variable is

| variable | description |
| -------- | ----------- |
| `teff` + `teff_err` | stellar effective temperature + uncertainty |

(called `response` and `response_err` in the `.Rdata` file) while the predictor variables are

| variable | description |
| -------- | ----------- |
| `ra_x` + `ra_error` | right ascension (celestial longitude) + uncertainty |
| `dec_x` + `dec_error` | declination (celestial latitude) + uncertainty |
| `parallax` + `parallax_error` | stellar parallax + uncertainty |
| `pmra` + `pmra_error` | proper motion along longitude line + uncertainty |
| `pmdec` + `pmdec_error` | proper motion along latitude line + uncertainty |
| `phot_[g,bp,rp]_mean_flux` + phot_[g,bp,rp]_mean_flux_error` | flux in green, blue, and red bands + uncertainties |
| `phot_[g,bp,rp]_mean_mag` | magnitudes in green, blue, and red bands + uncertainties |
| `bp_rp` | stellar color: blue band - red band magnitude |
| `L` + `B` | galactic longitude + latitude |

When starting off with these data, it would behoove you to extract a relatively small subsample both for EDA (< 10,000 stars) and for building models (< 100,000 stars). As your infrastructure falls into place, you can try applying models to the full dataset (via data splitting or cross-validation).

Now, you may notice that there is both redundant information and information that, at least at first blush, should not matter. The redundant information includes, e.g., `bp_rp`, since magnitudes are given, and (`L`,`B`), since galactic coordinates are just transformed celestial coordinates, etc. Redundancy is an issue primarily in linear regression analyses, where collinearity may crop up. ML algorithms by and large care not about redundancy. Regarding the information that seems like it should not matter: `parallax`, proper motion, etc...these are variables that indicate where a star is relative to us, and how it is moving across the sky relative to us, etc., and are not about the ball of gas itself. However, they might matter because interstellar dust affects our measurements of stellar light, and dust is inhomogeneously distributed, so including stellar location, etc., should improve temperature predictions.

