# Healthy Regions & Policies Lab

Visit [healthyregions.org](https://healthyregions.org) to learn about our recent projects and team. Here on Github you can explore all of our open source projects, and access some general data resources that we use internally.

<details>
  <summary><strong>HEROP_IDs</strong></summary>
  
  In some of our projects we use what we call a <strong>HEROP_ID</strong> to identify geographic boundaries defined by the US Census Bureau, which is a slight variation on the commonly used standard <strong>GEOID</strong>. Our format is similar to what the American FactFinder used (now data.census.gov). 

  A HEROP_ID consists of three parts:

  1. The 3-digit [Summary Level Code](https://www.census.gov/programs-surveys/geography/technical-documentation/naming-convention/cartographic-boundary-file/carto-boundary-summary-level.html) for this geography. Common summary level codes are:
      - `040` -- **State**
      - `050` -- **County**
      - `140` -- **Census Tract**
      - `150` -- **Census Block Group**
      - `860` -- **Zip Code Tabulation Area (ZCTA)**
  2. The 2-letter string `US`
  3. The standard [GEOID](https://www.census.gov/programs-surveys/geography/guidance/geo-identifiers.html) for the given unit (length depends on unit summary)
      - GEOIDs are, in turn, hierarchical aggregations of FIPS codes

  Expanding out the FIPS codes for the five summary levels shown above, the full IDs would look like:

  | summary level | format | length | example |
  |---|---|---|---|
  |State|`040US` + `STATE (2)`|7|`040US17` (Illinois)|
  |County|`050US` + `STATE (2)` + `COUNTY (3)`|10|`050US17019` (Champaign County)|
  |Tract|`140US` + `STATE (2)` + `COUNTY (3)` + `TRACT (6)`|16|`140US17019005900`|
  |Block Group|`150US` + `STATE (2)` + `COUNTY (3)` + `TRACT (6)` + `BLOCK GROUP (1)`|17|`150US170190059002`|
  |ZCTA|`860US` + `ZIP CODE (5)`|10|`860US61801`|

  The advantages of this composite ID are:
  
  1. Unique across all geographic areas in the US
  2. Will always be forced to string formatting
  3. Easy to programmatically change back into the more standard GEOIDs

  **Convert to GEOID (integers)**

  The `HEROP_ID` can be converted back to standard GEOIDs by removing the first 5 characters, or by taking everything after the substring "US". Here are some examples of what this looks like in different software:
  
  - Excel: `REPLACE(A1, 1, 5, "")`
  - R: `geoid <- str_split_i(HEROP_ID, "US", -1)`
  - Python: `geoid = HEROP_ID.split("US")[1]`
  - JavaScript: `const geoid = HEROP_ID.split("US")[1]`

</details>


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
    - Tip: `geopandas` should allow you to directly open remote zip files with something like this [learn more](https://geopandas.org/en/stable/docs/reference/api/geopandas.read_file.html):

            import geopandas as gpd
            gpd.read_file('/vsizip//vsicurl/https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/state-2010-shp.zip
  - **PMTiles** A "cloud-native" vector format that is very fast in the right web mapping environment [learn more](https://docs.protomaps.com/pmtiles/)

  ### Cartographic Boundaries 2010 (500k)
    
  |Geography|Format|Link|
  |---|---|---|
  |State|GeoJSON|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/state-2010-500k.geojson|
  |State|Shapefile (zip)|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/state-2010-500k-shp.zip|
  |State|PMTiles|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/state-2010-500k.pmtiles|
  |County|GeoJSON|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/county-2010-500k.geojson|
  |County|Shapefile (zip)|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/county-2010-500k-shp.zip|
  |County|PMTiles|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/county-2010-500k.pmtiles|
  |Tract|GeoJSON|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/tract-2010-500k.geojson|
  |Tract|Shapefile (zip)|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/tract-2010-500k-shp.zip|
  |Tract|PMTiles|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/tract-2010-500k.pmtiles|
  |Block group|GeoJSON|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/bg-2010-500k.geojson|
  |Block group|Shapefile (zip)|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/bg-2010-500k-shp.zip|
  |Block group|PMTiles|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/bg-2010-500k.pmtiles|

  *Note: We don't yet have ZCTA and Place geographies for 2010.*

  ### Cartographic Boundaries 2018 (500k)
  
  |Geography|Format|Link|
  |---|---|---|
  |State|GeoJSON|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/state-2018-500k.geojson|
  |State|Shapefile (zip)|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/state-2018-500k-shp.zip|
  |State|PMTiles|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/state-2018-500k.pmtiles|
  |County|GeoJSON|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/county-2018-500k.geojson|
  |County|Shapefile (zip)|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/county-2018-500k-shp.zip|
  |County|PMTiles|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/county-2018-500k.pmtiles|
  |ZCTA|GeoJSON|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/zcta-2010-500k.geojson|
  |ZCTA|Shapefile (zip)|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/zcta-2010-500k-shp.zip|
  |ZCTA|PMTiles|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/zcta-2010-500k.pmtiles|
  |Place|GeoJSON|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/place-2018-500k.geojson|
  |Place|Shapefile (zip)|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/place-2018-500k-shp.zip|
  |Place|PMTiles|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/place-2018-500k.pmtiles|
  |Tract|GeoJSON|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/tract-2018-500k.geojson|
  |Tract|Shapefile (zip)|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/tract-2018-shp.zip|
  |Tract|PMTiles|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/tract-2018-500k.pmtiles|
  |Block group|GeoJSON|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/bg-2018-500k.geojson|
  |Block group|Shapefile (zip)|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/bg-2018-500k-shp.zip|
  |Block group|PMTiles|https://herop-geodata.s3.us-east-2.amazonaws.com/oeps/bg-2018-500k.pmtiles|
  
</details>
