
Exoplanets, or extrasolar planets, are planets that exist outside of our Solar System. Due to their small size and their faintness, it is almost impossible to discover them via direct imaging; rather, they are discovered indirectly, most commonly via

- the radial velocity method, in which one detects a star's (relatively tiny)
wobble around its planetary system's center of mass; or

- the transit method, in which one detects an exoplanet passing in front of,
and thus partially eclipsing, its host star.

The transit method relies on a bit of luck: an exoplanet has to pass directly between us and the host star. That sort of chance alignment is rare. Hence for the transit method to be truly useful, we have to monitor *many* star systems.

The *Transiting Exoplanet Survey Satellite*, or *TESS*, launched in 2018, is designed to searth for exoplanets using (as you might guess) the transit method. It is surveying the brightest stars near the Earth. Unlike the earlier *Kepler* satellite, which fixated on a small region of the sky in the constellation of Cygnus, *TESS* is scanning nearly the full sky.

The dataset in this directory, downloaded on September 15, 2021, from

https://exoplanetarchive.ipac.caltech.edu/cgi-bin/TblView/nph-tblView?app=ExoTbls&config=TOI

has been processed so as to contain 3,393 *objects of interest*, of which

- 423 are confirmed planets (labeled `CP`);

- 490 are confirmed false positives (labeled `FP`); and

- 2480 are planetary candidates (labeled `PC`).

Your goal is to learn a classifier that disambiguates the confirmed planets and the confirmed false positives. At the end of the project, after the optimal classifier has been determined, you will apply it to the candidates to see how many you would predict are true exoplanets.

The predictor variables in this exercise are

| variables(s) | description |
| ---- | --------- |
| (ra,dec) | celestial longitude and latitude |
| (st_pmra,st_pmdec) | how "fast" the host star moves in the ra and dec directions (mas/yr) |
| pl_orbper | the planetary orbital period (days) |
| (pl_trandurh,pl_trandep) | the duration and "light-blocking amount" of the transit (hours and ppm) |
| pl_rade | the radius of the planet in Earth radii |
| pl_insol | the amount of light the planet receives, relative to what the Earth receives |
| pl_eqt | the planet's temperation (K) |
| st_tmag | the host star magnitude in the "TESS band" |
| st_dist | the distance to the host star, in parsecs |
| st_teff | the temperature of the host star (K) |
| st_logg | the host star's surface gravity (cm/s^2) |
| st_rad | the host star's radius, in solar radii |

The definition of each measurement is given [on this web page](https://exoplanetarchive.ipac.caltech.edu/docs/API_TOI_columns.html)

