# census-flows-mapper-viz
## Why 
Visualizing the longitudinal migration of people into the United States of America at the county level is just my idea of fun :)

[This visualization can be accessed here](https://flowmap.blue/1uGaROER7uvjlc9CyBHDELNzZatdgLrI9gJSQoEbcH3o)

![Census Flows Data visualized ](https://pbs.twimg.com/media/D-5YKpXWkAAl_oG.jpg)


## What
Visualizing data from Census Flows Mapper website https://flowsmapper.geo.census.gov/map.html#

via https://api.census.gov/data/2016/acs/flows.html

Migration flows are derived from the relationship between the location of current residence in the American Community Survey (ACS) sample and the responses given to the migration question "Where did you live 1 year ago?". There are flow statistics (moved in, moved out, and net moved) between county or minor civil division (MCD) of residence and county, MCD, or world region of residence 1 year ago. Estimates for MCDs are only available for the 12 strong-MCD states, where the MCDs have the same government functions as incorporated places. Migration flows between metropolitan statistical areas are available starting with the 2009-2016 5-year ACS dataset. In addition to the flow estimates, there are supplemental statistics files that contain migration/geographical mobility estimates (e.g., nonmovers, moved to a different state, moved from abroad) for each county, MCD, or metro area.	

## How

### FLOWS_data.zip
This file contains 7 datasets, each containing Flows data spanning the following survey years.

- 2006-2010
- 2007-2011
- 2008-2012
- 2009-2013
- 2010-2014
- 2011-2015
- 2012-2016

### get_data_from_census.sh
This script pulls all flows data for all counties for a single survey year
For example: ACS 5-year data `2012-2016` is `2016` in the below script

Change `YYYY` to the ending year of the survey dataset you want to pull
```curl -s "https://api.census.gov/data/YYYY/acs/flows?key=0a8afabaacd0aca63a1e6bfb384cb2a97c68ce56&get=MOVEDIN,MOVEDIN_M,GEOID2,COUNTY2_NAME,STATE2_NAME,COUNTY1_NAME,STATE1_NAME&for=county:013&in=state:01"| json2csv | sed 1,1d  >> YYYY_MASTER_IN.csv```

The files are of the following format:

|MOVEDIN|MOVEDIN_M|GEOID2|COUNTY2_NAME|STATE2_NAME|COUNTY1_NAME|STATE1_NAME|state|county|
|--|--|--|--|--|--|--|--|-|
|980|196|6037|Los Angeles County|California|Kings County|New York|36|47|

and describes flows FROM LA County, California --> Kings County (Brooklyn), New York.

A flow = The origin and destination combination of two counties for either migration or commuting. Each flow has at least three unweighted persons (i.e., movers).



### Full Metadata
Census Data API: Variables in /data/2016/acs/flows/variables			
Just discovered that this data has 66 variables but I've only used a few here.

|Name|Label|Required|Predicate Type|
|--|--|--|--|
|COUNTY1|FIPS county code of reference geography|not required|(not a predicate)|
|COUNTY1_NAME|FIPS county name of reference geography|not required|string|
|COUNTY2|FIPS county code of second geography|not required|int|
|COUNTY2_NAME|FIPS county name of second geography (blank for world region)|not required|string|
|for|Census API FIPS 'for' clause|predicate-only|fips-for|
|FROMABROAD|Movers from abroad|not required|int|
|FROMABROAD_M|Movers from abroad margin of error|not required|int|
|FROMDIFFCTY|Movers from different county, same state|not required|int|
|FROMDIFFCTY_M|Movers from different county, same state margin of error|not required|int|
|FROMDIFFMCD|Movers from different MCD, same state|not required|int|
|FROMDIFFMCD_M|Movers from different MCD, same state margin of error|not required|int|
|FROMDIFFMETRO|Movers from different metro area in the United States or Puerto Rico(supplemental statistic)|not required|int|
|FROMDIFFMETRO_M|Movers from different metro area in the United States or Puerto Rico margin of error|not required|int|
|FROMDIFFSTATE|Movers from different state|not required|int|
|FROMDIFFSTATE_M|Movers from different state margin of error|not required|int|
|FROMELSEWHEREUSPR|Movers from outside metro area in the United States or Puerto Rico (supplemental statistic)|not required|int|
|FROMELSEWHEREUSPR_M|Movers from outside metro area in the United States or Puerto Rico margin of error|not required|int|
|FULL1_NAME|Full name of reference geography|not required|(not a predicate)|
|FULL2_NAME|Full name of second geography|not required|(not a predicate)|
|GEOID1|Combined codes for the reference geography|not required|(not a predicate)|
|GEOID2|Combined codes for the second geography|not required|string|
|in|Census API FIPS 'in' clause|predicate-only|fips-in|
|MCD1|FIPS MCD code of reference geography|not required|(not a predicate)|
|MCD1_NAME|MCD name of reference geography|not required|string|
|MCD2|FIPS MCD code of second geography|not required|int|
|MCD2_NAME|MCD name of second geography (blank for world region)|not required|string|
|METRO1|Metropolitan statistical area code of reference geography|not required|(not a predicate)|
|METRO1_NAME|Metropolitan statistical area name of reference geography|not required|string|
|METRO2|Metropolitan statistical area code of second geography|not required|int|
|METRO2_NAME|Metropolitan statistical area name of second geography|not required|string|
|MOVEDIN|Total inbound migration to reference geography from second geography (flow statistic)|not required|(not a predicate)|
|MOVEDIN_M|Total inbound migration margin of error|not required|int|
|MOVEDNET|Total net migration|not required|(not a predicate)|
|MOVEDNET_M|Total net migration margin of error|not required|int|
|MOVEDOUT|Total outbound migration|not required|(not a predicate)|
|MOVEDOUT_M|Total outbound migration margin of error|not required|int|
|NONMOVERS|Same residence 1 year ago (nonmovers)|not required|int|
|NONMOVERS_M|Same residence 1 year ago (nonmovers) margin of error|not required|int|
|POP1YR|Population 1 year and over|not required|int|
|POP1YR_M|Population 1 year and over margin of error|not required|int|
|POP1YRAGO|Population living in county 1 year ago|not required|int|
|POP1YRAGO_M|Population living in county 1 year ago margin of error|not required|int|
|SAMECOUNTY|Movers within same county|not required|int|
|SAMECOUNTY_M|Movers within same county margin of error|not required|int|
|SAMEMCD|Movers within same MCD|not required|int|
|SAMEMCD_M|Movers within same MCD margin of error|not required|int|
|SAMEMETRO|Movers within same metro area (supplemental statistic)|not required|int|
|SAMEMETRO_M|Movers within same metro area margin of error|not required|int|
|STATE1|FIPS county code of reference geography|not required|int|
|STATE1_NAME|FIPS State name of reference geography|not required|string|
|STATE2|State code/world region code of second geography|not required|string|
|STATE2_NAME|State code/world region name of second geography|not required|string|
|SUMLEV1|Geographic summary level of reference geography|not required|int|
|SUMLEV2|Geographic summary level of second geography|not required|int|
|TODIFFCTY|Movers to different county, same state|not required|int|
|TODIFFCTY_M|Movers to different county, same state margin of error|not required|int|
|TODIFFMCD|Movers to different MCD, same state|not required|int|
|TODIFFMCD_M|Movers to different MCD, same state margin of error|not required|int|
|TODIFFMETRO|Movers to different metro area (supplemental statistic)|not required|int|
|TODIFFMETRO_M|Movers to different metro area margin of error|not required|int|
|TODIFFSTATE|Movers to different state|not required|int|
|TODIFFSTATE_M|Movers to different state margin of error|not required|int|
|TOELSEWHEREUSPR|Movers to outside metro area in the United States or Puerto Rico (supplemental statistic)|not required|int|
|TOELSEWHEREUSPR_M|Movers to outside metro area in the United States or Puerto Rico margin of error|not required|int|
|TOPUERTORICO|Movers to Puerto Rico|not required|int|
|TOPUERTORICO_M|Movers to Puerto Rico margin of error|not required|int


## Next Steps

Tableauing FROM-County_State --> TO-County_State

![image](https://user-images.githubusercontent.com/4397663/61172507-5943e080-a553-11e9-836c-44ffb667b55a.png)

![image](https://user-images.githubusercontent.com/4397663/61172512-652fa280-a553-11e9-9288-c18982e67954.png)
