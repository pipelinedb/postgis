# PipelineDB GIS Extension

This is a fork of [PostGIS](/postgis/postgis) that adds the capability of using GIS aggregates in [continuous views](http://docs.pipelinedb.com/continuous-views.html).

## Building

Install some dependencies first:

```
sudo apt-get install libxml2-dev libgeos-dev libproj-dev libgdal-dev xsltproc autoconf libtool libcunit1-dev
```

Make sure what `pipeline-config` is on your `PATH`. You can check that by running:

```
which pipeline-config
```

Now, you can build the extension libraries.

```
./autogen.sh
./configure
make
sudo make install
```

## Loading

Once you've installed the extension libraries, you can load the extension into a database by running:

```
-- Enable PostGIS (includes raster)
CREATE EXTENSION postgis;
-- Enable Topology
CREATE EXTENSION postgis_topology;
-- Enable PostGIS Advanced 3D
-- and other geoprocessing algorithms
-- sfcgal not available with all distributions
CREATE EXTENSION postgis_sfcgal;
-- fuzzy matching needed for Tiger
CREATE EXTENSION fuzzystrmatch;
-- rule based standardizer
CREATE EXTENSION address_standardizer;
-- example rule data set
CREATE EXTENSION address_standardizer_data_us;
-- Enable US Tiger Geocoder
CREATE EXTENSION postgis_tiger_geocoder;
```

## Testing

Start a PipelineDB instance on port `5432` and ensure that database `postgis_reg` does not exist. Run the following command:

```
make -s check
```
