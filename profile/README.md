# Healthy Regions & Policies Lab

Visit [healthyregions.org](https://healthyregions.org) to learn about our recent projects and team. Here on Github you can explore all of our open source projects, and access some general data resources that we use internally.

<details>
  <summary><strong>Download Census geography files</strong></summary>

  Within the backend of our [OEPS project](https://github.com/healthyregions/oeps) we have an ETL pipeline that merges, tranforms, and exports data files from the [US Census Bureau](https://www2.census.gov/geo/tiger/) into a few different geospatial data formats. There are two categories of files:
  
  - **Cartographic Boundaries** have simplified geometries which makes them ideal for mapping applications [learn more](https://www.census.gov/programs-surveys/geography/technical-documentation/naming-convention/cartographic-boundary-file.html)
    - We typically use the 500k scale files, though they publish other scales as well
  - **TIGER/Line Shapefiles** have official, unsimplified geometries and should be used for geospatial analysis [learn more](https://www.census.gov/geographies/mapping-files/time-series/geo/tiger-line-file.html)
    - *We don't have these in the pipeline yet, but hope to eventually...*
   
  Feel free to download and use these for your own projects.

  - **GeoJSON** A simple plain text format that is good for small to medium size datasets and can be used in a wide variety of web and desktop software [learn more](https://geojson.org/)
  - **Shapefiles** Used in scripting and desktop software for performant display and analysis [learn more](https://www.geographyrealm.com/what-is-a-shapefile/)
    - "Raw" shapefiles can be read remotely by `geopandas` (which is very cool) so we include them here. Use the zipped file if you are downloading for local use.
  - **PMTiles** A "cloud-native" vector format that is very fast in the right web mapping environment [learn more](https://docs.protomaps.com/pmtiles/)

  ### Cartographic Boundaries 2010 (500k)
    
  |Geography|Format|Link|
  |---|---|---|
  |State|GeoJSON|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/state-2010.geojson|
  |State|Shapefile (raw)|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/state-2010.shp|
  |State|Shapefile (zip)|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/state-2010-shp.zip|
  |State|PMTiles|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/state-2010.pmtiles|
  |County|GeoJSON|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/county-2010.geojson|
  |County|Shapefile (raw)|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/county-2010.shp|
  |County|Shapefile (zip)|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/county-2010-shp.zip|
  |County|PMTiles|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/county-2010.pmtiles|
  |Tract|GeoJSON|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/tract-2010.geojson|
  |Tract|Shapefile (raw)|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/tract-2010.shp|
  |Tract|Shapefile (zip)|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/tract-2010-shp.zip|
  |Tract|PMTiles|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/tract-2010.pmtiles|
  |Block group|GeoJSON|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/bg-2010.geojson|
  |Block group|Shapefile (raw)|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/bg-2010.shp|
  |Block group|Shapefile (zip)|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/bg-2010-shp.zip|
  |Block group|PMTiles|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/bg-2010.pmtiles|

  *Note: We don't yet have ZCTA and Place geographies for 2010.*

  ### Cartographic Boundaries 2018 (500k)
  
  |Geography|Format|Link|
  |---|---|---|
  |State|GeoJSON|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/state-2018.geojson|
  |State|Shapefile (raw)|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/state-2018.shp|
  |State|Shapefile (zip)|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/state-2018-shp.zip|
  |State|PMTiles|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/state-2018.pmtiles|
  |County|GeoJSON|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/county-2018.geojson|
  |County|Shapefile (raw)|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/county-2018.shp|
  |County|Shapefile (zip)|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/county-2018-shp.zip|
  |County|PMTiles|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/county-2018.pmtiles|
  |ZCTA|GeoJSON|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/zcta-2010.geojson|
  |ZCTA|Shapefile (raw)|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/zcta-2010.shp|
  |ZCTA|Shapefile (zip)|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/zcta-2010-shp.zip|
  |ZCTA|PMTiles|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/zcta-2010.pmtiles|
  |Place|GeoJSON|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/place-2018.geojson|
  |Place|Shapefile (raw)|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/place-2018.shp|
  |Place|Shapefile (zip)|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/place-2018-shp.zip|
  |Place|PMTiles|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/place-2018.pmtiles|
  |Tract|GeoJSON|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/tract-2018.geojson|
  |Tract|Shapefile (raw)|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/tract-2018.shp|
  |Tract|Shapefile (zip)|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/tract-2018-shp.zip|
  |Tract|PMTiles|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/tract-2018.pmtiles|
  |Block group|GeoJSON|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/bg-2018.geojson|
  |Block group|Shapefile (raw)|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/bg-2018.shp|
  |Block group|Shapefile (zip)|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/bg-2018-shp.zip|
  |Block group|PMTiles|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/bg-2018.pmtiles|
  
</details>
