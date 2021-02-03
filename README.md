
[![logo](logo.svg)](https://uclacovidbehindbars.org/)

# UCLA Law COVID-19 Behind Bars Data 

## Background 
The [UCLA Law COVID-19 Behind Bars Data Project](https://uclacovidbehindbars.org/), launched in March 2020, tracks the spread and impact of COVID-19 in American carceral facilities and advocates for greater transparency and accountability around the pandemic response of the carceral system. Since March, we have been collecting and reporting facility-level data on COVID-19 in prisons, jails, and other correctional centers. 

* **Latest data**: Our latest data on COVID-19 in jails and prisons is maintained in this repository [here](https://github.com/uclalawcovid19behindbars/data/tree/master/Adult%20Facility%20Counts).  
* **Historical data**: Our historical data is maintained in [our `historical-data` repository](https://github.com/uclalawcovid19behindbars/historical-data/tree/main/data). We are in the process of cleaning this data and will be adding additional states as this data becomes available. 
* **Additional data**: We also collect information about pandemic-related prison and jail releases, legal filings and court orders bearing on the safety of incarcerated people, and grassroots organizing campaigns and fundraisers [here](https://docs.google.com/spreadsheets/u/2/d/1X6uJkXXS-O6eePLxw2e4JeRtM41uPZ2eRcOA_HkPVTk/edit#gid=1641553906). 

## Our Process  
Our core dataset includes information on COVID-19 cases, deaths, and tests across more than 1,500 state, federal, and county facilities. We maintain this dataset by scraping and standardizing data from more than 80 sources. We scrape this data 3-4 times each week, although correctional agencies vary in how often they update their data. Our [scraper production code](https://github.com/uclalawcovid19behindbars/covid19_behind_bars_scrapers) and [more detailed documentation](https://uclalawcovid19behindbars.github.io/covid19-behind-bars-public-docs/scraper_documentation/) are available on GitHub. 

The majority of the facilities that we collect data on fall under state jurisdiction, where COVID-19 data is reported on state Department of Correction (DOC) websites. We also collect data from federal prisons reported by the [Federal Bureau of Prisons](https://www.bop.gov/coronavirus/) and from several large county jail systems – including [Los Angeles](https://lasd.org/covid19updates/), [New York City](https://www.nychealthandhospitals.org/correctionalhealthservices/), [Philadelphia](https://www.phila.gov/programs/coronavirus-disease-2019-covid-19/testing-and-data/#/philadelphia-prisons-covid-19-data), [Maricopa County](https://www.maricopa.gov/5574/COVID-19-in-County-Jails), [Orange County](https://ocsheriff.gov/about-ocsd/covid-19/covid-19-oc-jails), [Cook County](https://www.cookcountysheriff.org/covid-19-cases-at-ccdoc/), and [Hennepin County](https://www.hennepinsheriff.org/jail-warrants/jail-information/COVID-19). 

We are continuously adding to and refining our scrapers. Where possible, we have also retrospectively added COVID-19 data for facilities using digital archives. We are currently in the process of cleaning our historical scraped data and integrating population data to more readily compute COVID-19 rates across facilities over the course of the pandemic. This data is available for several states [here](https://github.com/uclalawcovid19behindbars/historical-data/tree/main/data). We are also developing an R package [`behindbarstools`](https://github.com/uclalawcovid19behindbars/behindbarstools), which includes a variety of functions to help pull, clean, wrangle, and visualize our data.  

**Contributors**: Our data for several jails in California is collected by [Davis Vanguard](https://www.davisvanguard.org/), who have been generously sharing their COVID-19 data with us. Our data for state prisons in Massachusetts is reported by [the ACLU of Massachusetts](https://data.aclum.org/sjc-12926-tracker/). If you would like to contribute data on COVID-19 in a facility that we don't currently include, please see [our template](https://docs.google.com/spreadsheets/d/1cqjCvbXuUh5aIQeJ4NRKdUwVAb4adaWTK-nBPFAj0og/edit#gid=363817589). We always welcome additional contributors! 

## Our Data 
Our core dataset includes the following metrics – reported separately for incarcerated people and staff at the facility level: 

* Cumulative COVID-19 cases 
* Cumulative COVID-19 deaths 
* Active COVID-19 cases 
* COVID-19 tests administered 

While we aim to collect facility-level data, not all jurisdictions report COVID-19 metrics at the facility level. Some DOCs only report statewide totals, and others do not report any data for certain metrics. Authorities also vary dramatically in how they define the metrics that they report. We do our best to standardize these variables, but comparing data across jurisdictions and over time should be done with caution. 

**Note**: Jurisdictions are continuously updating how, where, and whether they update their data. We do our best to accurately collect as much data as possible, but our data availability is subject to change. 

## Data Dictionary 
The full set of variables that we report includes the following: 

| Variable               | Description                                                                                                            |
|------------------------|------------------------------------------------------------------------------------------------------------------------|
| `Facility.ID`          | Integer ID that uniquely identifies every facility                                                                     |
| `Jurisdiction`         | Whether the facility falls under `state`, `county` or `federal` jurisdiction                                           |
| `State`                | State where the facility is located                                                                                    |
| `Name`                 | Facility name                                                                                                          |
| `Date`                 | Date data was scraped (not necessarily date updated by the reporting source)                                           |
| `source`               | Source from which the data was scraped                                                                                 |
| `Residents.Confirmed`  | Cumulative number of incarcerated individuals infected with COVID-19                                                   |
| `Staff.Confirmed`      | Cumulative number of staff infected with COVID-19                                                                      |
| `Residents.Deaths`     | Cumulative number of incarcerated individuals who died from COVID-19                                                   |
| `Staff.Deaths`         | Cumulative number of staff who died from COVID-19                                                                      |
| `Residents.Recovered`  | Cumulative number of incarcerated individuals who recovered from COVID-19                                              |
| `Staff.Recovered`      | Cumulative number of staff who recovered from COVID-19                                                                 |
| `Residents.Tadmin`     | Cumulative number of COVID-19 tests administered to incarcerated individuals                                           |
| `Staff.Tested`         | Cumulative number of staff tested for COVID-19                                                                         |
| `Residents.Negative`   | Cumulative number of incarcerated individuals who tested negative for COVID-19                                         |
| `Staff.Negative`       | Cumulative number of staff who tested negative for COVID-19                                                            |
| `Residents.Pending`    | Number of incarcerated individuals currently with pending test results for COVID-19                                    |
| `Staff.Pending`        | Number of staff currently with pending test results for COVID-19                                                       |
| `Residents.Quarantine` | Number of incarcerated individuals currently in quarantine from COVID-19                                               |
| `Staff.Quarantine`     | Number of staff currently in quarantine from COVID-19                                                                  |
| `Residents.Active`     | Number of incarcerated individuals currently infected with COVID-19                                                    |
| `Residents.Population` | Population of the facility as close to February 1, 2020 as possible.                                                   |
| `Address`              | The facility's address                                                                                                 |
| `Zipcode`              | The facility's zipcode                                                                                                 |
| `City`                 | The facility's city                                                                                                    |
| `County`               | The facility's county                                                                                                  |
| `Latitude`             | The facility's latitude                                                                                                |
| `Longitude   `         | The facility's longitude                                                                                               |
| `County.FIPS   `       | The facility's 5-digit county FIPS code                                                                                |
| `HIFLD.ID`             | The facility's corresponding [Homeland Infrastructure Foundation-Level Data](https://hifld-geoplatform.opendata.arcgis.com/datasets/prison-boundaries/data) ID |

## Citations

Citations for academic publications and research reports:

> Sharon Dolovich, Aaron Littman, Kalind Parish, Grace DiLaura, Chase Hommeyer,  Michael Everett, Hope Johnson, Neal Marquez, and Erika Tyagi. UCLA Law Covid-19 Behind Bars Data Project: Jail/Prison Confirmed Cases Dataset [date you downloaded the data]. UCLA Law, 2020, https://uclacovidbehindbars.org/.

Citations for media outlets, policy briefs, and online resources:

> UCLA Law Covid-19 Behind Bars Data Project, https://uclacovidbehindbars.org/.

## License 
Our data is licensed under a [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-nc-sa/4.0/). That means that you must give appropriate credit, provide a link to the license, and indicate if changes were made. You may not use our work for commercial purposes, which means anything primarily intended for or directed toward commercial advantage or monetary compensation. 
