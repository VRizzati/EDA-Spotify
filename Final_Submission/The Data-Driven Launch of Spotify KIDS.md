# The Data-Driven Launch of Spotify KIDS

Valentina Rizzati

## Abstract

***

For the launch of the new product Spotify KIDS, the Spotify marketing team asked for my support in prioritizing the areas where to run the Out-Of-Home (OOH) campaign so as to ensure we run a profitable (i.e. positive ROI defined as customer campaign value / marketing cost) marketing campaign. <br/>
I worked with [MTA turnstile data](http://web.mta.info/developers/turnstile.html) and with [Census data](https://data.census.gov/mdat/#/search?ds=ACSPUMS1Y2019) to first prioritize Public Use Microdata Areas (PUMAs) based on demographic targets provided by the Marketing team, and then select MTA stations based on foot traffic. Finally, by combining this information, I was able to narrow the MTA station list to the top 10 stations that should be targeted for the outdoor campaign.

## Design

***

Because of the limited amount of marketing budget, the main goal of the Marketing team is to run an efficient campaign, without overspending on the same individual. Therefore, I have decided to base the MTA station prioritization on the volume of unique individuals (UNIQUE TRAFFIC in the analysis) instead of the volume of impressions (TOTAL TRAFFIC in the analysis). Hence, UNIQUE TRAFFIC is the KPI I will optimize my model for. <br />

For reference, see below a few relevant metrics I have used to rank MTA stations:<br />
* TOTAL TRAFFIC = DAILY ENTRIES + DAILY EXITS
* COMMUTERS = x% * DAILY ENTRIES
* UNIQUE TRAFFIC = DAILY ENTRIES + DAILY EXITS - COMMUTERS
* TRAFFIC LEVEL: <br />
 * HIGH - 3rd tertile of TOTAL TRAFFIC
 * MED - 2nd tertile of TOTAL TRAFFIC
 * LOW - 1st tertile of TOTAL TRAFFIC

The final cluster of 10 MTA stations is the result of the following process:<br />
1. Identify PUMAs that match the demographic and socio-economic criteria provided by the marketing team 
  * Potentially narrow down the target list of PUMAs based on demographic and foot traffic considerations 
  * Within the final list of target PUMAs, determine which MTA stations present high UNIQUE TRAFFIC LEVEL
2. Identify other MTA stations that are close to the targeted PUMAs and that present high UNIQUE TRAFFIC LEVEL
3. Identify other MTA stations that, even if not in the selected PUMAs, present a high level of foot traffic and should be targeted for the purpose of this campaign

## Data

***

To identify the target MTA stations for the OOH campaign I used the following datasets:
* Census data to target PUMAs based on the following parameters:
 * Average Age > 30
 * Average Household income > USD 90k
 * Average Persons per Household > 2 
* MTA turnstile data to prioritize subway stations by foot traffic:
 * 12 weeks of data, from the week ending Jan 9th 2021 to the week ending Mar 27th 2021
 
From the Census data, I have gathered Average Age, Average Household income, and Average Persons per Household for all 55 PUMAs in NYC. 

From the MTA data, I have computed daily entries and exits for all 378 stations. This allowed me to compute the KPI that I intended to optimize the MTA station ranking for: UNIQUE TRAFFIC.

Finally, the geo data from the Google API was certainly instrumental to building the stations map. 

## Algorithms

***

*Data Cleaning* has been executed on the MTA data to remove duplicates, missing data and treat inconsistencies.

*Exploratory Data Analysis* has been conducted on both datasets to identify trends and identify the distribution of the data.

*Data Manipulation and Modeling* has been applied to both datasets:
* MTA data:
 * Create new columns representing common KPIs that are used when evaluating the location of a outdoor campaign 
 * Define ranking of MTA stations based on UNIQUE TRAFFIC
* Census data:
 * Append an additional column to the dataset to identify when a PUMA is in target for the campaign
 * Filter the list of PUMAs based on the conditions specified by the marketing team and produce a ranking of PUMAs
* Geo data:
 * Geolocate (latitude, longitude, altitude) all MTA stations by using geopy and the Google API 
 * Create Google map showing all MTA stations and color code them by traffic level

*Reconcile PUMAs and MTA stations rankings* by comparing the maps and selecting MTA stations with high foot traffic both within the targeted PUMAs and outside the targeted PUMAs but in high tarffic areas.

## Tools

***

* DB Browser for querying the data
* SQLAlchemy for a preliminary exploratory data analysis (EDA)
* Pandas for data cleaning, EDA, and data modeling
* Matplotlib and Seaborn for plotting
* Geopy, Gmaps and Google API for mapping

## Communication

***

The results were communicated in a presentation. In addition, see the MTA stations map below:<br />
* BLUE = high unique traffic
* ORANGE = medium unique traffic
* RED = low unique traffic

![Screen%20Shot%202021-04-29%20at%208.42.24%20PM.png](attachment:Screen%20Shot%202021-04-29%20at%208.42.24%20PM.png)
