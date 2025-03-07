#
# blockgrouphomevalues
#
###**Context*

A home purchase is among the most import decisions, and potentially risk investments, in a person's life. Their choice can reflect interest in long term gains, housing costs and, in the U.S., part of the American Dream. Analytics of home values and rental costs, however, are commonly limited to highest level geographic aggregates and broad, even annual, periods of time.

This publication produces a data file shared in the Block Groups Datasets dataverse hosted on https://dataverse.harvard.edu/dataverse/blockgroupdatasets. The data is shared under a Common Commons, open source license, without warranties, share alike, non commercial and by attribution.

###*Method*

This publication attempts to cast home values down to U.S. Census block group geographies, by inheriting and averaging the measures from ZIP code level estimates. On the whole, block groups with a few hundred households are considerably smaller than ZIP code areas with several thousand. In addition, the two geographies are managed by separate Federal agencies, the U.S. Postal Service and the Census Bureau, so they are  inherently dissimilar. The simplest method of projection involves overlaying the two geographies, having a block group inherit the estimates of the ZIP code level that covers it. When the block group spans ZIP code boundaries, an average is appropriate, weighted by land area lying in each parent. 

###*Data*
Zillow is recognized as an innovator in predicting home values, serving real estate agents, home buyers, and home sellers. Their research service publishes several estimates at a ZIP code level including measures of home value (Zillow Home Value Index ZHVI) and rental costs (Zillow Observed Rent Index ZORI). The ZHVI is broken down by housing type: single family homes and condominiums. And, each of their publications has monthly frequency dating, in some cases, to 2000.
 
Block group geographic boundariess are maintained by the US Census' TIGER (Topologically Integrated Geographic Encoding and Referencing) 
publication. ZIP code boundaries are not generally published, but shared from a private company, Dotlas, in various retail marketing solutions.

ZIP codes, also, have long been problematic for demographic analytics. Their boundaries span counties and states, so you cannot tiethem to familar geographies including Census tracts and block groups. The Census Bureau tries to address this by using ZIP Code Tabulation Areas (ZCTAs). These are coded very much like 5 digit ZIP codes and are equal to them most of the time. When A ZIP code geography crosses a county line, though, new ZCTAs are invented to represent each side of the split area. So, while ZIP codes cannot be aggregated, ZCTAs can total into counties, states, divisions and regions.

The blockgrouphomevalues dataset offers the following columns
---------------------------------------------------------------------------------------------------------------------------------
|Column|Data Type|Description|
---------------------------------------------------------------------------------------------------------------------------------
|STATEFP|string|The 2-digit State FIPS code of the block group|
|COUNTYFP|string|The 3-digit County FIPS code of the block group|
|TRACTCE|string|The 6-digit Census Tract of the block group|
|BLKGRPCE|string|The 1-digit Block Group of the block group|
|GEOID|string|12 digit concatenation of State, County, Tract and Block Group codes|
|GEOIDFQ|string|The 'fully qualified' GEOID with US country prefix|
|ALAND|integer|The land area if the block group in square meters|
|AWATER|integer|The area if the block group, covered by water, in square meters|
|INTPTLAT|float|Latitude of the block groups centroid point|
|INTPTLON|float|Longitude of the block groups centroid point|
|ZIP Codes Overlaying|list|List of the ZIP codes that overlay the block group|
|ZHVI All Housing Types|float|Zillow Home Value Index, attributed to the block group, all housing types|
|ZHVI Single Family Homes|float|Zillow Home Value Index, attributed to the block group, single family homes|
|ZHVI Condos/Coops|float|Zillow Home Value Index, attributed to the block group, condominiums and cooperatively owned|
|ZORI All Housing Types|float|Zillow Observed Rent Index, attributed to the block group|
---------------------------------------------------------------------------------------------------------------------------------
###Additional Notes

 * When the Block Group Code BLKGRPCE is '0', that block group is under water. Block groups cover the Great Lakes, for example, making a confusing visual for chloropleth maps.
 * To support visualization, the code also uses Census definitions of cities called Combined Statitical Areas, which group counties together.  The CSA for New York includes 22 counties, distinguished as Central or Outlying. The Delineation Files publication includes the geographic IDs of state and county FIPS codes in each major city.
 * Maps of these results may be visually biased. New York City and San Francisco Bay areas have extreme housing values, but they have small land areas.  Denver by contrast has higher then median housing values with very large land areas. As a result, western Colorado looks like the dominating location of home values.
 * When more than one ZIP code overlays a block group, values are attributed by the shared land area. This assumes that housing is uniform over the block group and related ZIP code areas.

###Citations:

“Housing Data.” Zillow, Zillow Group, Inc., 13 Feb. 2025, www.zillow.com/research/data/. 
“ZIP Code to ZCTA Crosswalk.” HCP GeoCare Navigator, United States Health Resources & Services Administration, https://data.hrsa.gov/DataDownload/GeoCareNavigator/ZIP%20Code%20to%20ZCTA%20Crosswalk.xlsx. Accessed 28 Feb. 2025. 
"ZACTA Shape files", United States Census Bureau, TIGER/Line, 2024, https://www2.census.gov/geo/tiger/TIGER2024/ZCTA520/tl_2024_us_zcta520.zip	
"Block Group Shape files", United States Census Bureau, TIGER/Line, 2024, https://www2.census.gov/geo/tiger/TIGER2024/BG/*.zip
“United States Zipcode Boundaries with Shapefiles / GeoJSON (US Zips)”, Marketplace, Databricks, Inc., Publisher is https://www.dotlas.com/, 1 Mar. 2025, https://www.databricks.com/product/marketplace
"Delineation Files for Combined Statistical Areas", United States Census Bureau, https://www.census.gov/geographies/reference-files/time-series/demo/metro-micro/delineation-files.html, Accessed 7 March 2025
