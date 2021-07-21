
[![logo](logo.svg)](https://uclacovidbehindbars.org/)

# UCLA Law COVID Behind Bars Data 

The [UCLA Law COVID Behind Bars Data Project](https://uclacovidbehindbars.org/), launched in March 2020, tracks the spread and impact of COVID in American carceral facilities and advocates for greater transparency and accountability around the pandemic response of the carceral system. Since March, we have been collecting and reporting facility-level data on COVID in prisons, jails, and other correctional centers. 

## About Our Data 

Our core dataset includes information on COVID cases, deaths, tests, and vaccinations across more than 1,700 state, federal, county, and immigration correctional facilities. We maintain this dataset by scraping and standardizing data from 100+ sources. Our [scraper production code](https://github.com/uclalawcovid19behindbars/covid19_behind_bars_scrapers) is available on GitHub. We are also developing an R package [`behindbarstools`](https://github.com/uclalawcovid19behindbars/behindbarstools), which includes a variety of functions to help pull, wrangle, and visualize our data. We strongly recommend using this package to access our data. 

The majority of the facilities that we collect data on are state prisons, where COVID data is reported on Department of Correction (DOC) websites. We also collect data from federal prisons reported by the [Federal Bureau of Prisons (BOP)](https://www.bop.gov/coronavirus/), immigration detention centers reported by [Immigrations and Customs Enforcement (ICE)](https://www.ice.gov/coronavirus) and from several large county jail systems – including [Los Angeles](https://lasd.org/covid19updates/), [New York City](https://www.nychealthandhospitals.org/correctionalhealthservices/), [Philadelphia](https://www.phila.gov/programs/coronavirus-disease-2019-covid-19/testing-and-data/#/philadelphia-prisons-covid-19-data), [Maricopa County](https://www.maricopa.gov/5574/COVID-19-in-County-Jails), [Orange County](https://ocsheriff.gov/about-ocsd/covid-19/covid-19-oc-jails), [Cook County](https://www.cookcountysheriff.org/covid-19-cases-at-ccdoc/), and [Hennepin County](https://www.hennepinsheriff.org/jail-warrants/jail-information/COVID-19). We also collect data on juvenile detention facilities and state psychiatric facilities where available. 

**June 2021 update**: In response to less frequent data updates from correctional agencies, we will only scrape and publish data twice weekly (down from 3-4 times weekly). We will continue archiving raw files from 100+ sources 3 times weekly, but we will not publish this data at the same frequency. 

## Directory Structure

The directory tree below summarises the data files that we maintain in this repository: 

```
data/
    |— latest-data/
    |   |— latest_facility_counts.csv
    |   |— latest_state_counts.csv
    |   |— latest_national_counts.csv
    |   |– latest_state_jurisdiction_counts.csv 
    |— historical-data/
    |   |— historical_facility_counts.csv
    |   |— historical_state_counts.csv
    |   |— historical_national_counts.csv
    |   |– historical_state_jurisdiction_counts.csv 
    |– anchored-data/
    |   |— state_population_counts.csv 
```

Files in the `latest-data` directory include only the most recent counts based on our latest scraped data, while files in the `historical-data` directory include all historical time-series data that we've collected since the start of the pandemic. The files in `anchored-data` include population data that we update on a monthly basis to use as denominators when calculating rates. 

## Data Files & Dictionaries     

#### `_facility_counts.csv`
* **Row definition**: Each row represents a unique facility (or the most granular level of aggregation reported by an agency). 
* **Facilities included**: Includes adult and juvenile state facilities, federal facilities, immigration detention facilities, county jail systems, and state psychiatric facilities. This file only includes information that we collect directly from agency websites.

| Variable               | Description                                                                                                       
|------------------------|-------------------------------------------------------------------------------------------------------------------|
| `Facility.ID`          | Integer ID that uniquely identifies each facility. Additional facility-level information can be linked to the data files in [this repo](https://github.com/uclalawcovid19behindbars/facility_data) based on this ID | 
| `Jurisdiction`         | Whether the facility falls under `state`, `county`, `federal`, `immigration`, or `psychiatric` jurisdiction       |
| `State`                | State where the facility is located                                                                               |
| `Name`                 | Facility name                                                                                                     |
| `Date`                 | Date data was scraped (not necessarily date updated by the reporting source)                                      |
| `Source`               | Source(s) from which the data was scraped                                                                         |
| `Residents.Confirmed`  | Cumulative number of incarcerated individuals infected with COVID                                                 |
| `Staff.Confirmed`      | Cumulative number of staff infected with COVID                                                                    |
| `Residents.Deaths`     | Cumulative number of incarcerated individuals who died from COVID                                                 |
| `Staff.Deaths`         | Cumulative number of staff who died from COVID                                                                    |
| `Residents.Tadmin`     | Cumulative number of COVID tests administered to incarcerated individuals                                         |
| `Residents.Tested`     | Cumulative number of incarcerated individuals tested for COVID                                                    |
| `Residents.Active`     | Number of incarcerated individuals currently infected with COVID                                                  |
| `Staff.Active`         | Number of staff currently infected with COVID                                                                     |
| `Population.Feb20`     | Population of the facility as close to February 2020 as possible                                                  |
| `Residents.Population` | Current population of incarcerated individuals (most recent data available)                                       |
| `Residents.Initiated`  | Cumulative number of incarcerated individuals who have received at least one dose of a vaccine                    |
| `Staff.Initiated`      | Cumulative number of staff who have received at least one dose of a vaccine                                       |
| `Residents.Completed`  | Cumulative number of incarcerated individuals who are fully vaccinated                                            |
| `Staff.Completed`      | Cumulative number of staff who are fully vaccinated                                                               |
| `Residents.Vadmin`     | Cumulative number of vaccine doses administered to incarcerated individuals                                       |
| `Staff.Vadmin`         | Cumulative number of vaccine doses administered to staff                                                          |
| `Web.Group`            | One of `Prison` (state adult facilities), `Federal` (BOP facilities), `ICE` (ICE facilities), `Juvenile` (state and local youth facilities), `Psychiatric` (state psychiatric facilities), or `County` (county jails) | 

We also include the following geographic fields: `Address`, `Zipcode`, `City`, `County`, `Latitude`, `Longitude`, `County.FIPS`.

#### `_state_counts.csv`
* **Row definition**: Each row represents a state prison agency (DOC), with federal (BOP) and immigration (ICE) totals reported as separate rows. 
* **Facilities included**: Includes adult and juvenile state facilities, federal facilities, and immigration detention facilities. Data from county jails and state psychiatric facilities are NOT included in these aggregates, as our data for these facilities is not comprehensive. This file supplements information reported directly on agency websites with statewide totals collected by [The Marshall Project](https://www.themarshallproject.org/2020/05/01/a-state-by-state-look-at-coronavirus-in-prisons).

| Variable               | Description                                                                                                        |
|------------------------|--------------------------------------------------------------------------------------------------------------------|
| `State`                | State agency, `Federal`, or `ICE`                                                                                  |
| `Residents.Confirmed`  | Cumulative number of incarcerated individuals infected with COVID                                                  |
| `Staff.Confirmed`      | Cumulative number of staff infected with COVID                                                                     |
| `Residents.Deaths`     | Cumulative number of incarcerated individuals who died from COVID                                                  |
| `Staff.Deaths`         | Cumulative number of staff who died from COVID                                                                     |
| `Residents.Tadmin`     | Cumulative number of COVID tests administered to incarcerated individuals                                          |
| `Residents.Tested`     | Cumulative number of incarcerated individuals tested for COVID                                                     |
| `Residents.Active`     | Number of incarcerated individuals currently infected with COVID                                                   |
| `Staff.Active`         | Number of staff currently infected with COVID                                                                      |
| `Residents.Initiated`  | Cumulative number of incarcerated individuals who have received at least one dose of a vaccine                     |
| `Staff.Initiated`      | Cumulative number of staff who have received at least one dose of a vaccine                                        |
| `Residents.Completed`  | Cumulative number of incarcerated individuals who are fully vaccinated                                             |
| `Staff.Completed`      | Cumulative number of staff who are fully vaccinated                                                                |
| `Residents.Vadmin`     | Cumulative number of vaccine doses administered to incarcerated individuals                                        |
| `Staff.Vadmin`         | Cumulative number of vaccine doses administered to staff                                                           |
| `Residents.Population` | Current population of incarcerated individuals (most recent data available)                                        |
| `Staff.Population`     | Current population of staff (most recent data available)                                  			              |

#### `_national_counts.csv`
* **Row definition**: Each row represents a COVID metric. 
* **Facilities included**: Includes adult and juvenile state facilities, federal facilities, and immigration detention facilities. Data from county jails and state psychiatric facilities are NOT included in these aggregates, as our data for these facilities is not comprehensive. This file supplements information reported directly on agency websites with statewide totals collected by [The Marshall Project](https://www.themarshallproject.org/2020/05/01/a-state-by-state-look-at-coronavirus-in-prisons).

| Variable               | Description                                                                                                        |
|------------------------|--------------------------------------------------------------------------------------------------------------------|
| `Measure`              | COVID variable (as defined in the dictionaries above)                                                              |
| `Count`                | Total reported by state and federal agencies (including 51 DOCs, BOP, and ICE)                                     |
| `Reporting`            | Number of agencies included in the total (of 53 agencies)                                                          |
| `Missing`              | List of agencies that do not report data for the given measure (not included in the total)                         |

#### `_state_jurisdiction_counts.csv`
* **Row definition**: Each row represents a unique combination of `State`, `Web.Group`, and `Measure`.  
* **Facilities included**: Includes adult and juvenile state facilities, federal facilities, immigration detention facilities, county jail systems, and state psychiatric facilities. This file supplements information reported directly on agency websites with statewide totals collected by [The Marshall Project](https://www.themarshallproject.org/2020/05/01/a-state-by-state-look-at-coronavirus-in-prisons).

| Variable               | Description                                                                                                        |
|------------------------|--------------------------------------------------------------------------------------------------------------------|
| `State`                | State where the facility is located                                                                                |
| `Web.Group`            | One of `Prison` (state adult facilities), `Federal` (BOP facilities), `ICE` (ICE facilities), `Juvenile` (state and local youth facilities), `Psychiatric` (state psychiatric facilities), or `County` (county jails) |
| `Measure`              | COVID variable (as defined in the dictionaries above)                                                              |
| `Val`                  | Total reported by facilities in a state of the given `Web.Group` type                                              |
| `Rate`                 | Estimated rate based on a population denominator of February 2020                                                  |
| `Date`                 | Date data was scraped (not necessarily date updated by the reporting source)                                       |

#### `_state_jurisdiction_counts.csv`
* **Row definition**: Each row represents a unique combination of `State`, `Web.Group`, and `Measure`.  
* **Facilities included**: Includes adult and juvenile state facilities, federal facilities, immigration detention facilities, county jail systems, and state psychiatric facilities. This file supplements information reported directly on agency websites with statewide totals collected by [The Marshall Project](https://www.themarshallproject.org/2020/05/01/a-state-by-state-look-at-coronavirus-in-prisons).

| Variable               | Description                                                                                                        |
|------------------------|--------------------------------------------------------------------------------------------------------------------|
| `State`                | State where the facility is located                                                                                |
| `Web.Group`            | One of `Prison` (state adult facilities), `Federal` (BOP facilities), `ICE` (ICE facilities), `Juvenile` (state and local youth facilities), `Psychiatric` (state psychiatric facilities), or `County` (county jails) |
| `Measure`              | COVID variable (as defined in the dictionaries above)                                                              |
| `Val`                  | Total reported by facilities in a state of the given `Web.Group` type                                              |
| `Rate`                 | Estimated rate based on a population denominator of February 2020                                                  |
| `Date`                 | Date data was scraped (not necessarily date updated by the reporting source)                                       |

#### `state_population_counts.csv`
* **Row definition**: Each row represents a state prison agency (DOC), with federal (BOP) and immigration (ICE) totals reported as separate rows.
* **Facilities included**: Includes adult and juvenile state facilities, federal facilities, and immigration detention facilities.

| Variable               | Description                                                                                                        |
|------------------------|--------------------------------------------------------------------------------------------------------------------|
| `State`                | State agency, Federal, or ICE                                                                                      |
| `Residents.Population` | Current population of incarcerated individuals (most recent data available at the beginning of each month)         |
| `Staff.Population`     | Current population of staff (most recent data available at the beginning of each month)                            |
| `Date`                 | Date (month and year) updated                                                                                      |

We aim to collect population data as of the first day of each month (i.e. `july2021` would correspond to July 1, 2021), but data may be older depending on when an agency last reported data. When agencies do not publicly report data, we supplement this file with information collected directly through public records requests, along with data reported by The [Vera Institute for Justice](https://www.vera.org/publications/people-in-jail-and-prison-in-spring-2021) and [The Marshall Project](https://www.themarshallproject.org/2020/05/01/a-state-by-state-look-at-coronavirus-in-prisons). 

## Citations

Citations for academic publications and research reports:

> Sharon Dolovich, Aaron Littman, Kalind Parish, Grace DiLaura, Chase Hommeyer,  Michael Everett, Hope Johnson, Neal Marquez, and Erika Tyagi. UCLA Law Covid-19 Behind Bars Data Project: Jail/Prison Confirmed Cases Dataset [date you downloaded the data]. UCLA Law, 2020, https://uclacovidbehindbars.org/.

Citations for media outlets, policy briefs, and online resources:

> UCLA Law Covid-19 Behind Bars Data Project, https://uclacovidbehindbars.org/.

## License 

Our data is licensed under a [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-nc-sa/4.0/). That means that you must give appropriate credit, provide a link to the license, and indicate if changes were made. You may not use our work for commercial purposes, which means anything primarily intended for or directed toward commercial advantage or monetary compensation. 

## Contributors 

For questions or feedback about the data, please reach out to Michael Everett (everett@law.ucla.edu), Hope Johnson (johnsonh@law.ucla.edu), Neal Marquez (marquezn@law.ucla.edu), and Erika Tyagi (tyagi@law.ucla.edu). 

In cases when agencies do not publicly report comprehensive data for all facilities in a state, we supplement our data with statewide aggregate totals collected through public records requests, data collected by [The Marshall Project and the AP](https://www.themarshallproject.org/2020/05/01/a-state-by-state-look-at-coronavirus-in-prisons), and other sources. Our data for several jails in California is collected by the [COVID In-Custody Project](https://covidincustody.org/). Our data for facilities in Massachusetts is reported by [the ACLU of Massachusetts](https://data.aclum.org/sjc-12926-tracker/). If you would like to contribute data on COVID in a facility that we don't currently include, please see [our template](https://docs.google.com/spreadsheets/d/1cqjCvbXuUh5aIQeJ4NRKdUwVAb4adaWTK-nBPFAj0og/edit#gid=363817589). 
