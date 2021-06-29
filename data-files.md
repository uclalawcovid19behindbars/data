# Data files 
**Note**: these files are on the `jur_agg` branch of out data repo right now – we’ll start writing them to the `master` and `website` branches soon! 

* `adult_facility_covid_counts.csv`  
	* **Uses**: homepage facility table (HO), states page facility tables (HO) 
	* **Rows**: facility 
	* **Universe**: full scraped data (does NOT include MP integrated data) 
* `national_aggregate_counts.csv` 
	* **Uses**: main Google Sheet 
	* **Rows**: metrics 
	* **Universe**: does NOT include psychiatric or county jurisdiction, DOES include juvenile state (not juvenile county though), DOES include MP integrated data 
* `state_aggregate_counts.csv` - state and federal totals 
	* **Uses**: vaccine table on homepage (HO) 
	* **Rows**: states, separate rows for Federal and ICE 
	* **Universe**: does NOT include psychiatric or county jurisdiction, DOES include juvenile state (not juvenile county though), DOES include MP integrated data 
* `state_jurisdiction_aggregate_counts.csv` 
	* **Uses**: state page totals (HO), CDC dashboard  
	* **Rows**: `State` + `Web.Group` + `Measure` combination 
	* **Universe**: everything (including MP integrated data) 

The web groups in the jurisdiction aggregate file include the following: 
* `Prison`: Adults in state prisons
* `Federal`: Adults in federal prisons 
* `ICE`: People in ICE facilities
* `County`: (dropped)
* `Juvenile`: Youth in state and local facilities 
* `Psychiatric`: Adults in state psychiatric facilities 