
[![logo](logo.svg)](https://uclacovidbehindbars.org/)

# UCLA Law COVID-19 Behind Bars Data 

The [UCLA Law COVID-19 Behind Bars Data Project](https://uclacovidbehindbars.org/), launched in March 2020, tracks the spread and impact of COVID-19 in American carceral facilities and advocates for greater transparency and accountability around the pandemic response of the carceral system. Since March, we have been collecting and reporting facility-level data on COVID-19 in prisons, jails, and other correctional centers. 

Our latest data is maintained in this repository. Instructions for accessing our historical time-series data are provided [below](https://github.com/uclalawcovid19behindbars/data#accessing-time-series-data). 

## About Our Data 

**June 2021 update**: In response to fewer and fewer data updates from correctional agencies, we will only scrape and publish data twice weekly (this is down from 3-4 times weekly). We will continue scraping raw files from 100+ sources 3 times weekly for safe-keeping, but we will not clean, harmonize, and publish this data at the same frequency. 

Our core dataset includes information on COVID-19 cases, deaths, tests, and vaccinations across more than 1,700 state, federal, county, and immigration correctional facilities. We maintain this dataset by scraping and standardizing data from 100+ sources. Our [scraper production code](https://github.com/uclalawcovid19behindbars/covid19_behind_bars_scrapers) and [more detailed documentation](https://uclalawcovid19behindbars.github.io/covid19-behind-bars-public-docs/scraper_documentation/) are available on GitHub. We are continuously adding to and refining our scrapers. Where possible, we have also retrospectively added COVID-19 data for facilities using digital archives.  

The majority of the facilities that we collect data on are state prisons, where COVID-19 data is reported on Department of Correction (DOC) websites. We also collect data from federal prisons reported by the [Federal Bureau of Prisons (BOP)](https://www.bop.gov/coronavirus/), immigration detention centers reported by [Immigrations and Customs Enforcement (ICE)](https://www.ice.gov/coronavirus) and from several large county jail systems – including [Los Angeles](https://lasd.org/covid19updates/), [New York City](https://www.nychealthandhospitals.org/correctionalhealthservices/), [Philadelphia](https://www.phila.gov/programs/coronavirus-disease-2019-covid-19/testing-and-data/#/philadelphia-prisons-covid-19-data), [Maricopa County](https://www.maricopa.gov/5574/COVID-19-in-County-Jails), [Orange County](https://ocsheriff.gov/about-ocsd/covid-19/covid-19-oc-jails), [Cook County](https://www.cookcountysheriff.org/covid-19-cases-at-ccdoc/), and [Hennepin County](https://www.hennepinsheriff.org/jail-warrants/jail-information/COVID-19). We also collect data on state psychiatric facilities. 

## Data Files 
Our project aims to collect facility-level COVID-19 data. However some agencies do not report data for all facilities, leaving some gaps in statewide aggregate totals. When we are unable to collect comprehensive data for all facilities within a state, we supplement our data with statewide aggregate totals collected through public records requests, data collected by [The Marshall Project and the AP](https://www.themarshallproject.org/2020/05/01/a-state-by-state-look-at-coronavirus-in-prisons), and other publicly available sources. As a result, we maintain three files: 

| File | Description |
|-|-|
| `adult_facility_covid_counts.csv` | Facility-level data from state facilities (collected from state DOCs), federal facilities (collected from the BOP), immigration detention facilities (collected from ICE), and several county jail systems. This dataset only includes information that we collect directly from agency websites. |
| `state_aggregate_counts.csv` | State-aggregated data from state facilities, along with federal and immigration totals reported as separate rows. Data from county jails is NOT included in these aggregates because our data from county jails is not comprehensive. This dataset supplements information reported on agency websites with statewide aggregate totals reported by other sources including The Marshall Project and the AP. |
| `national_aggregate_counts.csv` | Nationally-aggregated data from state, federal, and immigration facilities based on the same set of sources as the state-aggregated file. This dataset also reports the number of agencies reporting each metric and lists the agencies that are missing from each total. |

## Data Dictionary 

The set of variables that we report includes the following: 

| Variable               | Description                                                                                                                    |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| `Facility.ID`          | Integer ID that uniquely identifies every facility                                                                             |
| `Jurisdiction`         | Whether the facility falls under `state`, `county`, `federal`, `immigration`, or `psychiatric` jurisdiction                    |
| `State`                | State where the facility is located                                                                                            |
| `Name`                 | Facility name                                                                                                                  |
| `Date`                 | Date data was scraped (not necessarily date updated by the reporting source)                                                   |
| `Source`               | Source from which the data was scraped                                                                                         |
| `Residents.Confirmed`  | Cumulative number of incarcerated individuals infected with COVID-19                                                           |
| `Staff.Confirmed`      | Cumulative number of staff infected with COVID-19                                                                              |
| `Residents.Deaths`     | Cumulative number of incarcerated individuals who died from COVID-19                                                           |
| `Staff.Deaths`         | Cumulative number of staff who died from COVID-19                                                                              |
| `Residents.Tadmin`     | Cumulative number of COVID-19 tests administered to incarcerated individuals                                                   |
| `Residents.Tested`     | Cumulative number of incarcerated individuals tested for COVID-19                                                              |
| `Residents.Active`     | Number of incarcerated individuals currently infected with COVID-19                                                            |
| `Staff.Active`         | Number of staff currently infected with COVID-19                                                                               |
| `Population.Feb20`     | Population of the facility as close to February 2020 as possible                                                               |
| `Residents.Population` | Current population of incarcerated individuals reported by agency website                                                      |
| `Residents.Initiated`  | Cumulative number of incarcerated individuals who have received at least one dose of a COVID-19 vaccine                        |
| `Staff.Initiated`      | Cumulative number of staff who have received at least one dose of a COVID-19 vaccine                                           |
| `Residents.Completed`  | Cumulative number of incarcerated individuals who are fully vaccinated                                                         |
| `Staff.Completed`      | Cumulative number of staff who are fully vaccinated                                                                            |
| `Residents.Vadmin`     | Cumulative number of COVID-19 vaccine doses administered to incarcerated individuals                                           |
| `Staff.Vadmin`         | Cumulative number of COVID-19 vaccine doses administered to staff                                                              |
| `HIFLD.ID`             | The facility's corresponding [Homeland Infrastructure Foundation-Level Data](https://hifld-geoplatform.opendata.arcgis.com/datasets/prison-boundaries/data) ID |

We also include the following geographic fields: `Address`, `Zipcode`, `City`, `County`, `Latitude`, `Longitude`, `County.FIPS`.

**Note**: Jurisdictions are continuously updating how, where, and whether they update their data. We do our best to accurately collect as much data as possible, but our data availability is subject to change. Authorities also vary dramatically in how they define the metrics that they report. We do our best to standardize these variables, but comparing data across jurisdictions and over time should be done with caution. 

## Accessing Time-Series Data 

This repository contains the latest values that we scraped for a given facility. We are currently in the process of cleaning our full historical time-series data and integrating population data to more readily compute COVID-19 rates across facilities over the course of the pandemic. 

This data can be downloaded in `csv` format [here](http://104.131.72.50:3838/scraper_data/summary_data/scraped_time_series.csv). 

We are developing an R package [`behindbarstools`](https://github.com/uclalawcovid19behindbars/behindbarstools), which includes a variety of functions to help pull, clean, wrangle, and visualize our data. We strongly recommend using this package to access our latest data. 

To access time-series data in R: 
```
devtools::install_github("uclalawcovid19behindbars/behindbarstools")

data <- behindbarstools::read_scrape_data(all_dates = TRUE)
```

To access time-series data in Python:  
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

For questions or feedback about the data, please reach out to Michael Everett (everett@law.ucla.edu), Hope Johnson (johnsonh@law.ucla.edu), Neal Marquez (marquezn@law.ucla.edu), and Erika Tyagi (tyagi@law.ucla.edu). 

Our data for several jails in California is collected by [Davis Vanguard](https://www.davisvanguard.org/), who have been generously sharing their COVID-19 data with us. Our data for state prisons in Massachusetts is reported by [the ACLU of Massachusetts](https://data.aclum.org/sjc-12926-tracker/). If you would like to contribute data on COVID-19 in a facility that we don't currently include, please see [our template](https://docs.google.com/spreadsheets/d/1cqjCvbXuUh5aIQeJ4NRKdUwVAb4adaWTK-nBPFAj0og/edit#gid=363817589). We always welcome additional contributors! 
