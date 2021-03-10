
[![logo](logo.svg)](https://uclacovidbehindbars.org/)

# UCLA Law COVID-19 Behind Bars Data 

The [UCLA Law COVID-19 Behind Bars Data Project](https://uclacovidbehindbars.org/), launched in March 2020, tracks the spread and impact of COVID-19 in American carceral facilities and advocates for greater transparency and accountability around the pandemic response of the carceral system. Since March, we have been collecting and reporting facility-level data on COVID-19 in prisons, jails, and other correctional centers. 

* **Latest data**: Our latest COVID-19 data is maintained in this repository. 
* **Historical data**: Our historical data is maintained in [our `historical-data` repository](https://github.com/uclalawcovid19behindbars/historical-data/tree/main/data). We are in the process of cleaning this data and will be adding additional states as this data becomes available. 
* **Additional data**: We also collect information about pandemic-related prison and jail releases, legal filings and court orders bearing on the safety of incarcerated people, and grassroots organizing campaigns and fundraisers [here](https://docs.google.com/spreadsheets/u/2/d/1X6uJkXXS-O6eePLxw2e4JeRtM41uPZ2eRcOA_HkPVTk/edit#gid=1641553906). 

## About Our Data 

Our core dataset includes information on COVID-19 cases, deaths, and tests across more than 1,700 state, federal, county, and immigration correctional facilities. We collect additional information based on what agencies report (e.g. population data and vaccination data). We maintain this dataset by scraping and standardizing data from more than 120 sources. We scrape this data 3-4 times each week, although correctional agencies vary in how often they update their data. Our [scraper production code](https://github.com/uclalawcovid19behindbars/covid19_behind_bars_scrapers) and [more detailed documentation](https://uclalawcovid19behindbars.github.io/covid19-behind-bars-public-docs/scraper_documentation/) are available on GitHub. We are continuously adding to and refining our scrapers. Where possible, we have also retrospectively added COVID-19 data for facilities using digital archives.  

The majority of the facilities that we collect data on fall under state jurisdiction, where COVID-19 data is reported on state Department of Correction (DOC) websites. We also collect data from federal prisons reported by the [Federal Bureau of Prisons (BOP)](https://www.bop.gov/coronavirus/), immigration detention centers reported by [Immigrations and Customs Enforcement (ICE)](https://www.ice.gov/coronavirus) and from several large county jail systems – including [Los Angeles](https://lasd.org/covid19updates/), [New York City](https://www.nychealthandhospitals.org/correctionalhealthservices/), [Philadelphia](https://www.phila.gov/programs/coronavirus-disease-2019-covid-19/testing-and-data/#/philadelphia-prisons-covid-19-data), [Maricopa County](https://www.maricopa.gov/5574/COVID-19-in-County-Jails), [Orange County](https://ocsheriff.gov/about-ocsd/covid-19/covid-19-oc-jails), [Cook County](https://www.cookcountysheriff.org/covid-19-cases-at-ccdoc/), and [Hennepin County](https://www.hennepinsheriff.org/jail-warrants/jail-information/COVID-19). 

Our project aims to collect facility-level COVID-19 data. However some agencies do not report data for all facilities, leaving some gaps in statewide aggregate totals. When we are unable to collect comprehensive data for all facilities within a state, we supplement our data with statewide aggregate totals collected through public records requests, data collected by [The Marshall Project](https://www.themarshallproject.org/2020/05/01/a-state-by-state-look-at-coronavirus-in-prisons), and other publicly available sources. As a result, we maintain three files: 

| File | Description |
|-|-|
| `adult_facility_covid_counts.csv` | Facility-level data from state facilities (collected from state DOCs), federal facilities (collected from the BOP), immigration detention facilities (collected from ICE), and several county jail systems. This dataset only includes information directly reported on agency websites. |
| `state_aggregate_counts.csv` | State-aggregated data from state facilities, along with federal and immigration totals reported as separate rows. Data from county jails is NOT included in these aggregates because our data from county jails is not comprehensive. This includes data reported directly on agency websites, along with statewide aggregate totals reported from other sources. |
| `national_aggregate_counts.csv` | Nationally-aggregated data from state, federal, and immigration facilities. This dataset also reports the number of agencies reporting each metric and lists the agencies that are missing from each aggregated metric.  |

**Note**: Jurisdictions are continuously updating how, where, and whether they update their data. We do our best to accurately collect as much data as possible, but our data availability is subject to change. Authorities also vary dramatically in how they define the metrics that they report. We do our best to standardize these variables, but comparing data across jurisdictions and over time should be done with caution. 

## Data Dictionary 

The full set of variables that we report includes the following: 

| Variable               | Description                                                                                                                    |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| `Facility.ID`          | Integer ID that uniquely identifies every facility                                                                             |
| `Jurisdiction`         | Whether the facility falls under `state`, `county`, `federal`, or `immigration` jurisdiction                                   |
| `State`                | State where the facility is located                                                                                            |
| `Name`                 | Facility name                                                                                                                  |
| `Date`                 | Date data was scraped (not necessarily date updated by the reporting source)                                                   |  
| `Source`               | Source from which the data was scraped                                                                                         |
| `Residents.Confirmed`  | Cumulative number of incarcerated individuals infected with COVID-19                                                           |
| `Staff.Confirmed`      | Cumulative number of staff infected with COVID-19                                                                              |
| `Residents.Deaths`     | Cumulative number of incarcerated individuals who died from COVID-19                                                           |
| `Staff.Deaths`         | Cumulative number of staff who died from COVID-19                                                                              |
| `Residents.Recovered`  | Cumulative number of incarcerated individuals who recovered from COVID-19                                                      |
| `Staff.Recovered`      | Cumulative number of staff who recovered from COVID-19                                                                         |
| `Residents.Tadmin`     | Cumulative number of COVID-19 tests administered to incarcerated individuals                                                   |
| `Staff.Tested`         | Cumulative number of staff tested for COVID-19                                                                                 |
| `Residents.Negative`   | Cumulative number of incarcerated individuals who tested negative for COVID-19                                                 |
| `Staff.Negative`       | Cumulative number of staff who tested negative for COVID-19                                                                    |
| `Residents.Pending`    | Number of incarcerated individuals currently with pending test results for COVID-19                                            |
| `Staff.Pending`        | Number of staff currently with pending test results for COVID-19                                                               |
| `Residents.Quarantine` | Number of incarcerated individuals currently in quarantine from COVID-19                                                       |
| `Staff.Quarantine`     | Number of staff currently in quarantine from COVID-19                                                                          |
| `Residents.Active`     | Number of incarcerated individuals currently infected with COVID-19                                                            |
| `Population.Feb20`     | Population of the facility as close to February 1, 2020 as possible                                                            |
| `Residents.Population` | Current population of incarcerated individuals reported by agency website                                                      |
| `Residents.Tested`     | Cumulative number of incarcerated individuals tested for COVID-19                                                              |
| `Residents.Initiated`  | Cumulative number of incarcerated individuals who have initiated COVID-19 vaccination (i.e. received any dosage of a vaccine)  |
| `Residents.Completed`  | Cumulative number of incarcerated individuals who have fully completed their COVID-19 vaccination schedule                     |
| `Residents.Vadmin`     | Cumulative number of COVID-19 vaccines administered to incarcerated individuals                                                |
| `Staff.Initiated`      | Cumulative number of staff who have initiated COVID-19 vaccination (i.e. received any dosage of a vaccine)                     |
| `Staff.Completed`      | Cumulative number of staff who have fully completed their COVID-19 vaccination schedule                                        |
| `Staff.Vadmin`         | Cumulative number of COVID-19 vaccines administered to staff                                                                   |
| `Address`              | The facility's address                                                                                                         |
| `Zipcode`              | The facility's zipcode                                                                                                         |
| `City`                 | The facility's city                                                                                                            |
| `County`               | The facility's county                                                                                                          |
| `Latitude`             | The facility's latitude                                                                                                        |
| `Longitude`            | The facility's longitude                                                                                                       |
| `County.FIPS`          | The facility's 5-digit county FIPS code                                                                                        |
| `HIFLD.ID`             | The facility's corresponding [Homeland Infrastructure Foundation-Level Data](https://hifld-geoplatform.opendata.arcgis.com/datasets/prison-boundaries/data) ID |

## Accessing Our Data 

This repository contains the latest values that we scraped for a given facility. We are currently in the process of cleaning our full historical time series data and integrating population data to more readily compute COVID-19 rates across facilities over the course of the pandemic. This data is available for several states [here](https://github.com/uclalawcovid19behindbars/historical-data/tree/main/data). All of our time series data since November is available [here](http://104.131.72.50:3838/scraper_data/summary_data/scraped_time_series.csv). 

We are developing an R package [`behindbarstools`](https://github.com/uclalawcovid19behindbars/behindbarstools), which includes a variety of functions to help pull, clean, wrangle, and visualize our data. We recommend using this package to access our latest data. 

To access post-November time series data in R: 
```
devtools::install_github("uclalawcovid19behindbars/behindbarstools")

data <- behindbarstools::read_scrape_data(all_dates = TRUE, coalesce = TRUE)
```

To access post-November time series data in Python:  
```
import pandas as pd 

data = pd.read_csv("http://104.131.72.50:3838/scraper_data/summary_data/scraped_time_series.csv")
```

## Citations

Citations for academic publications and research reports:

> Sharon Dolovich, Aaron Littman, Kalind Parish, Grace DiLaura, Chase Hommeyer,  Michael Everett, Hope Johnson, Neal Marquez, and Erika Tyagi. UCLA Law Covid-19 Behind Bars Data Project: Jail/Prison Confirmed Cases Dataset [date you downloaded the data]. UCLA Law, 2020, https://uclacovidbehindbars.org/.

Citations for media outlets, policy briefs, and online resources:

> UCLA Law Covid-19 Behind Bars Data Project, https://uclacovidbehindbars.org/.

## License 

Our data is licensed under a [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-nc-sa/4.0/). That means that you must give appropriate credit, provide a link to the license, and indicate if changes were made. You may not use our work for commercial purposes, which means anything primarily intended for or directed toward commercial advantage or monetary compensation. 

## Contributors 

For questions or feedback about the data, please to reach out to [Michael Everett](everett@law.ucla.edu), [Hope Johnson](johnsonh@law.ucla.edu), [Neal Marquez](marquezn@law.ucla.edu), and [Erika Tyagi](tyagi@law.ucla.edu). 

Our data for several jails in California is collected by [Davis Vanguard](https://www.davisvanguard.org/), who have been generously sharing their COVID-19 data with us. Our data for state prisons in Massachusetts is reported by [the ACLU of Massachusetts](https://data.aclum.org/sjc-12926-tracker/). If you would like to contribute data on COVID-19 in a facility that we don't currently include, please see [our template](https://docs.google.com/spreadsheets/d/1cqjCvbXuUh5aIQeJ4NRKdUwVAb4adaWTK-nBPFAj0og/edit#gid=363817589). We always welcome additional contributors! 
