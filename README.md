# R-CORE


This system is based on the version of the System R Plus and RH-Mex for its execution through a terminal. 

This repository describes the syntax of the parameters to be used and a couple of examples are added to test the functionality.

---

## Sintaxis R-CORE
Argument definition

|Field|Available Values|Comments|
|---|---|---|
|Configuration File (JSON)|"{file}"|"/home/hiar/SwissRe/r-core/config.json"| 
|Process Type|L, LC, LS |L=Load Portfolio, LC=Load and Compute, LS=Load and Summaries| 
|Initial Chunk|numeric|1| 
|Total Chunks|numeric|2| 
|---|---|---|

## Configuration File

This file allows us to define the input files, as well as the result path, the system path where the application is located, among other properties which are described below:


```
{
	"Perils":"S",
	"CutOffDate":"2020-10-20",
	"Portfolios": [
		{
		"FileName": "/home/hiar/SwissRe/R_Core/account.csv",d
		"Type": 7
		},
		{
		"FileName": "/home/hiar/SwissRe/R_Core/location.csv",
		"Type": 8
		},
		{
		"FileName": "/home/hiar/SwissRe/R_Core/reinsInfo.csv",
		"Type": 9
		},
		{
		"FileName": "/home/hiar/SwissRe/R_Core/reinsScope.csv",
		"Type": 10
		}
  	],
	"ResultsPath":"/home/hiar/SwissRe/R_Core/results",
	"SystemPath":"/home/hiar/SwissRe/R_Core/R-Core",
}
```

## JSON parameters
---

|Field|Available Values|Comments|
|---|---|---|
|Perils|S, SR, H|S=Earthquake, SR=Earthquake (Regulatory), H=Hydro| 
|Cutoff Date|yyyy-MM-dd|2020-10-30|
|Portfolios|["{Filename, Type}"]|Array of Portfolios {Filename, Type}|
|Results Path | "{path}" | "/home/hiar/SwissRe/rcore/Tests" |
|SystemPath|"{path}"| System path for R-Core or RH-Mex Core |
|Tr|String| List of Tr separated by commas |
|ScenarioInfo|{IdScenario,Peril,Filename,URL}| Info required for Scenario evaluation |
|---|---|---|

### Portfolio Types
|Type|Portfolio|
|---|---|
|7 |Account File|
|8 |Location File|
|9 |Reinsurance Info|
|10 |Reinsurance Scope|
|---|---|

---

# Examples

## Example of a portfolio evaluation

In the case of simple evaluation, only the Account and Location files are required.


```
{
	"Perils":"S",
	"CutOffDate":"2020-10-20",
	"Portfolios": [
		{
		"FileName": "/home/hiar/SwissRe/R_Core/acc.csv",
		"Type": 7
		},
		{
		"FileName": "/home/hiar/SwissRe/R_Core/loc.csv",
		"Type": 8
		}
  	],
	"ResultsPath":"/home/hiar/SwissRe/R_Core/results",
	"SystemPath":"/home/hiar/SwissRe/R_Core/R-Core"
}
```
---

## Example with Reinsurance Files

When conducting an evaluation with reinsurance schemes, it will be necessary to add two new files, ReinsuranceInfo and ReinsurancScope to our Portfolio list as shown below.


```
{
	"Perils":"S",
	"CutOffDate":"2020-10-20",
	"Portfolios": [
		{
		"FileName": "/home/hiar/SwissRe/R_Core/acc.csv",
		"Type": 7
		},
		{
		"FileName": "/home/hiar/SwissRe/R_Core/loc.csv",
		"Type": 8
		},
		{
		"FileName": "/home/hiar/SwissRe/R_Core/reinsInfo.csv",
		"Type": 9
		},
		{
		"FileName": "/home/hiar/SwissRe/R_Core/reinsScope.csv",
		"Type": 10
		}
  	],
	"ResultsPath":"/home/hiar/SwissRe/R_Core/results",
	"SystemPath":"/home/hiar/SwissRe/R_Core/R-Core"
}
```

## Example of Scenario evaluation

In the case of scenario evaluation, we must enter the information corresponding to the scenario ID, the hazard and in case a zip file is provided, the name of the file.


```
{
	"Perils":"S",
	"Portfolios": [
		{
		"FileName": "/home/hiar/SwissRe/R_Core/acc.csv",
		"Type": 7
		},
		{
		"FileName": "/home/hiar/SwissRe/R_Core/loc.csv",
		"Type": 8
		}
  	],
	"ResultsPath":"/home/hiar/SwissRe/R_Core/results",
	"SystemPath":"/home/hiar/SwissRe/R_Core/R-Core",
	"ScenarioInfo":
	{
		"IdScenario" : 10602,
		"Peril": "QEQ"
	}
}
```
If you wish to evaluate an event through the catalog provided by ERN, you must indicate the URL of the event contained in the ERN servers or, if you have the event (in zip format), you can enter it as follows:

* Computation by URL
```
{
	"Perils":"S",
	"Portfolios": [
		{
		"FileName": "/home/hiar/SwissRe/R_Core/acc.csv",
		"Type": 7
		},
		{
		"FileName": "/home/hiar/SwissRe/R_Core/loc.csv",
		"Type": 8
		}
  	],
	"ResultsPath":"/home/hiar/SwissRe/R_Core/results",
	"SystemPath":"/home/hiar/SwissRe/R_Core/R-Core",
	"ScenarioInfo":
	{		
		"Peril": "QEQ",
		"URL": "https://serv.ern.com.mx/download/Escenarios/2022/02%20SISMO/SISMO_eq20221211.zip"
	}
}
```

* Computation by File (in zip format - provided by ERN)
```
{
	"Perils":"S",
	"Portfolios": [
		{
		"FileName": "/home/hiar/SwissRe/R_Core/acc.csv",
		"Type": 7
		},
		{
		"FileName": "/home/hiar/SwissRe/R_Core/loc.csv",
		"Type": 8
		}
  	],
	"ResultsPath":"/home/hiar/SwissRe/R_Core/results",
	"SystemPath":"/home/hiar/SwissRe/R_Core/R-Core",
	"ScenarioInfo":
	{		
		"Peril": "QEQ",
		"Filename": "/home/hiar/SwissRe/R_Core/SISMO_eq20221211.zip"
	}
}
```



---


# Execution

The execution cycle consists of three main phases: Load, Evaluation and Results, these stages are defined by the processType parameter and each process consists of the following:
1. Portfolio loading, in this process the validation of the entered information is performed to detect if there are any errors, warnings or any kind of inconsistency in the information we are entering.
2. Computing, in this process the evaluation of the portfolio is carried out and this can be divided into N processes to optimise the time of the evaluation, the N processes executed will depend on the RAM and processor cores of the equipment.
3. Results, in the last process the accumulation of the results obtained by each calculation process is carried out and then the result files are written.

R-Core

```sh
#First step, Load the  Portfolio
dotnet "R_Core.dll" "/home/hiar/SwissRe/Examples/cfg_eq.json" "L" 1 1 

#Second, the Calculation, in this example we divide the computing process in 2 subprocess
dotnet "R_Core.dll" "/home/hiar/SwissRe/Examples/cfg_eq.json" "LC" 1 2
dotnet "R_Core.dll" "/home/hiar/SwissRe/Examples/cfg_eq.json" "LC" 2 2

#Finally, the Accumulation and Summarize process to get results 
dotnet "R_Core.dll" "/home/hiar/SwissRe/Examples/cfg_eq.json" "LS" 1 2
```

In order to carry out the evaluation of a scenario, it will only be necessary to execute the loading of the portfolio, as well as a single process with the parameter "esc" (this method does not allow the multiple execution of N processes).

```sh
#First step, Load the  Portfolio
dotnet "R_Core.dll" "/home/hiar/SwissRe/Examples/cfg_eq.json" "L" 1 1 

#Finally, the Scenario Evaluation 
dotnet "R_Core.dll" "/home/hiar/SwissRe/Examples/cfg_eq.json" "esc" 1 1
```
---

# Results Types

The systems produce different types of results, the results updated with the latest updates by our team, the results that are generated through the R Plus System (our current commercial version) and the regulatory results. In order to obtain these results, it will be necessary to run the corresponding executables.

</br>

* Updated Results: The updated results are obtained with the ASLAC (Amenaza Sismica de Latinoamerica y Caribe - Seismic Hazards of Latin America and the Caribbean) system. The R-Core system (ASLAC - EQ) is used, as well as the R-Core ASLAC system files.

* R Plus Results: The R Plus System results are obtained with the R-Core system (MX, COL - EQ & HYDRO) as well as the R-Core system files.

* Regulatory Results: In this case the RH-Mex Core applications are used for hydrometeorological phenomena results and the R-Core for earthquake. For earthquake it will be necessary to assign the value of "SR" in the "Perils" field of the configuration file (json).

---
</br>

# Downloads

In the following links you can find the latest stable version of the system for downloading

* R-Core (MX, COL - EQ & HYDRO) v2.0.0.2 (8 MB) [download](https://serv.ern.com.mx/download/SwissRe_PATM/R_Core_v2.0.0.2_linux-x64.zip) (updated 2023-08-28)

* R-Core File System v2.0.0.1 (821 MB) [download](https://serv.ern.com.mx/download/SwissRe_PATM/R_Core_fs_v2.0.0.1.zip) (updated 2023-03-28)

* R-Core (ASLAC - EQ) v2.0.0.2 (8 MB) [download](https://serv.ern.com.mx/download/SwissRe_PATM/R_Core_v2.0.0.2_ASLAC_linux-x64.zip) (updated 2023-08-28)
  
* R-Core ASLAC File System v2.0.0.1 (745 MB) [download](https://serv.ern.com.mx/download/SwissRe_PATM/R_Core_fs_v2.0.0.1_ASLAC.zip) (updated 2023-05-23)


* RH-Mex Core v2.0.0.1 (3 MB) [download](https://serv.ern.com.mx/download/SwissRe_PATM/RH-Mex_Core_v2.0.0.0_linux-x64.zip) (updated 2023-03-28)

* RH-Mex Core File System v2.0.0.1 (166 MB) [download](https://serv.ern.com.mx/download/SwissRe_PATM/RH-Mex_Core_fs_v2.0.0.0.zip) (updated 2023-03-28)
