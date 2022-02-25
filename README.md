# R-CORE

This system is based on the version of the System R Plus and RH-Mex for its execution through a series of parameters through a terminal. 

In the following links you can find a compressed files which contains a folder with all the files necessary for its execution. 

This repository describes the syntax of the parameters to be used and a couple of examples are added to test the functionality.

## Links

* R-Core (5 MB) [download](https://serv.ern.com.mx/download/SwissRe_PATM/R_Core_v1.0.0.15_linux-x64.zip) (updated 2022-01-11)

* R-Core File System (534 MB) [download](https://serv.ern.com.mx/download/SwissRe_PATM/R_Core_fs_v1.0.0.15.zip) (updated 2022-01-11)


* RH-Mex Core (2 MB) [download](https://serv.ern.com.mx/download/SwissRe_PATM/RH-Mex_Core_v1.0.0.4_linux-x64.zip) (updated 2022-01-11)

* RH-Mex Core File System (166 MB) [download](https://serv.ern.com.mx/download/SwissRe_PATM/RH-Mex_Core_v1.0.0.4_fs.zip) (updated 2022-01-11)

## Sintaxis R-CORE
Argument definition

|Field|Available Values|Comments|
|---|---|---|
|Configuration File (JSON)|"{file}"|"/home/hiar/SwissRe/r-core/config.json"| 
|Process Type|L, LC, LS |L=Load Portfolio, LC=Load and Compute, LS=Load and Accumulate| 
|Initial Chunk|numeric|1| 
|Total Chunks|numeric|2| 
|---|---|---|

## Configuration File

Most of the arguments from the previous version were integrated into this json file 

```sh
{
	"Perils":"S",
	"CutOffDate":"2020-10-20",
	"Portfolios": [
		{
		"FileName": "/home/hiar/SwissRe/R_Core/EQ_Ind.csv",
		"Type": 1
		},
		{
		"FileName": "/home/hiar/SwissRe/R_Core/policies.csv",
		"Type": 2
		},
		{
		"FileName": "/home/hiar/SwissRe/R_Core/buildings.csv",
		"Type": 2
		}
  	],
	"ResultsPath":"/home/hiar/SwissRe/R_Core/results",
	"SystemPath":"/home/hiar/SwissRe/R_Core/R-Core"
}
```

### JSON parameters

|Field|Available Values|Comments|
|---|---|---|
|Perils|S, SR, H|S=Earthquake, SR=Earthquake (Regulatory), H=Hydro| 
|Cutoff Date|yyyy-MM-dd|2020-10-30|
|Portfolios|["{Filename, Type}"]|Array of Portfolios {Filename, Type -> 1 = Individual, 2 = Collective}|
|Results Path|"{path}"|"/home/hiar/SwissRe/rcore/Tests"|
|SystemPath|"{path}"| System path for R-Core or RH-Mex Core |
|---|---|---|


## Examples

### Example (R-Core - Collective Portfolio) 


In the case of collective portfolios, two files are required, one with the information of the policies and the other with the information of the buildings and both must be integrated with Type=2, internally the system will determine through its column scheme which corresponds to each table as previously handled in XML.


Configuration file
```sh
{
	"Perils":"S",
	"CutOffDate":"2020-10-20",
	"Portfolios": [
		{
		"FileName": "/home/hiar/SwissRe/R_Core/Ej_policies.csv",
		"Type": 2
		},
		{
		"FileName": "/home/hiar/SwissRe/R_Core/EJ_blds.csv",
		"Type": 2
		}
  	],
	"ResultsPath":"/home/hiar/SwissRe/R_Core/results",
	"SystemPath":"/home/hiar/SwissRe/R_Core/R-Core"
}
```

### Example (R-Core - Individual) 

Independent portfolio assessment for earthquake

Configuration file
```sh
{
	"Perils":"S",
	"CutOffDate":"2020-10-20",
	"Portfolios": [
		{
		"FileName": "/home/hiar/SwissRe/R_Core/buildings.csv",
		"Type": 1
		}
  	],
	"ResultsPath":"/home/hiar/SwissRe/R_Core/results",
	"SystemPath":"/home/hiar/SwissRe/R_Core/R-Core"
}
```
### Execution

R-Core

```sh
#In each execution the process type must be changed in the configuration file
#ProcessType = L
dotnet "R_Core.dll" "/home/hiar/SwissRe/Examples/cfg_eq.json" "L" 1 1 

#ProcessType = LC
dotnet "R_Core.dll" "/home/hiar/SwissRe/Examples/cfg_eq.json" "LC" 1 2
dotnet "R_Core.dll" "/home/hiar/SwissRe/Examples/cfg_eq.json" "LC" 2 2

#ProcessType = LS
dotnet "R_Core.dll" "/home/hiar/SwissRe/Examples/cfg_eq.json" "LS" 1 2


```

RH-Mex

```sh
#In each execution the process type must be changed in the configuration file

#ProcessType = L
dotnet "RH-Mex_core.dll" "/home/hiar/SwissRe/Examples/cfg_RH.json" "L" 1 1 

#ProcessType = LC
dotnet "RH-Mex_core.dll" "/home/hiar/SwissRe/Examples/cfg_rh.json" "LC" 1 2 
dotnet "RH-Mex_core.dll" "/home/hiar/SwissRe/Examples/cfg_rh.json" "LC" 2 2 

#ProcessType = LS
dotnet "RH-Mex_core.dll" "/home/hiar/SwissRe/Examples/cfg_rh.json" "LS" 1 2 
```
