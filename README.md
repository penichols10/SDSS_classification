# Introduction

In this repository, a model is trained to identify objects from the Sloan Digital Sky Survey as galaxies, stars, or quasars. The hope was actually that the data would be a bit more messy or the model a bit harder to fit.

# Data Source
SDSS has a [tool](http://skyserver.sdss.org/dr17/SearchTools/sql) that allows users to download data from their Data Release 17 for free using SQL queries. I ran a simple query to download data about as many objects as possible, specifically positional data, spectral data, and related data to identify information about the photography process. The query is below:

SELECT
p.objid,p.ra,p.dec,p.u,p.g,p.r,p.i,p.z,
p.run, p.rerun, p.camcol, p.field,
s.specobjid, s.class, s.z as redshift,
s.plate, s.mjd, s.fiberid
FROM PhotoObj AS p
JOIN SpecObj AS s ON s.bestobjid = p.objid
WHERE 
  p.u BETWEEN 0 AND 19.6
  AND g BETWEEN 0 AND 20