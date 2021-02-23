# R-CORE

This system is based on the version of the System R Plus and RH-Mex for its execution through a series of parameters through a terminal. 

In the following links you can find a compressed files which contains a folder with all the files necessary for its execution. 

This repository describes the syntax of the parameters to be used and a couple of examples are added to test the functionality.

## Links

* miniR (2 MB) [download](https://serv.ern.com.mx/download/SwissRe_PATM/miniR_v1.0.0.3_linux_x64.zip) (updated 2021-02-22)

* miniR File System (706 MB) [download](https://serv.ern.com.mx/download/SwissRe_PATM/miniR_fs.zip) (updated 2021-02-03)


* RH-Mex core (510 KB) [download](https://serv.ern.com.mx/download/SwissRe_PATM/RH-Mex_core_linux-x64.zip) (updated 2021-02-03)

* RH-Mex File System (166 MB) [download](https://serv.ern.com.mx/download/SwissRe_PATM/rh_fs.zip) (updated 2021-02-03)

## Sintaxis R-CORE
Argument definition

|Field|Available Values|Comments|
|---|---|---|
|Configuration File (JSON)|"{file}"|"/home/hiar/SwissRe/r-core/config.json"| 
|Initial Chunk|numeric|1| 
|Total Chunks|numeric|2| 
|---|---|---|

## Configuration File

Most of the arguments from the previous version were integrated into this json file 

```sh
{
	"ProcessType":"L",
	"Perils":"H",
	"CutOffDate":"2020-10-20",
	"PortfolioType":3,
	"Portfolios":["/home/hiar/SwissRe/r-core/Ind_test.xml", "/home/hiar/SwissRe/r-core/Col_test.xml"],
	"ResultsPath":"/home/hiar/SwissRe/r-core/results",
	"SystemPath":"/home/hiar/SwissRe/r-core/miniR_fs"
}
```

### JSON parameters

|Field|Available Values|Comments|
|---|---|---|
|ProcessType|L, LM, LC, LS |L=Load Portfolio, *LM=Load Portfolio bin to Memory, LC=Load and Compute, LS=Load and Accumulate| 
|Perils|S, SR, H|S=Earthquake, SR=Earthquake (Regulatory), H=Hydro| 
|Cutoff Date|yyyy-MM-dd|2020-10-30|
|PortfolioType|1, 2, 3|1=Individual,2=Collective,3=Both (3 - just for miniR)|
|Portfolios|["{file}"]|When PortfolioType = 3, two file names must be entered; otherwise only one|
|Results Path|"{path}"|"/home/hiar/SwissRe/rcore/Tests"|
|SystemPath|"{path}"| System path for miniR or RH-Mex |
|---|---|---|

### LM Process 

* Improve portfolio loading across all processes.
* The LM process must be alive as long as the N LC and LS processes are running.
* When the LM process finishes loading the portfolio to memory, it generates a PortfolioID.id file with a unique identifier, in case the process fails, a text file with the corresponding error is generated.
* Once the LC and LS processes have finished, the process that executed the LM command must be killed.
* Only available for R Plus (miniR) 


## Examples

### Example (miniR - Individual and Collective) 

Configuration file
```sh
{
	"ProcessType":"L",
	"Perils":"S",
	"CutOffDate":"2020-12-30",
	"PortfolioType":3,
	"Portfolios":["/home/hiar/SwissRe/r-core/Ind_test.xml", "/home/hiar/SwissRe/r-core/Col_test.xml"],
	"ResultsPath":"/home/hiar/SwissRe/r-core/results",
	"SystemPath":"/home/hiar/SwissRe/r-core/miniR_fs"
}
```

### Example (miniR - Individual) 

Independent portfolio assessment for earthquake

Configuration file
```sh
{
	"ProcessType":"L",
	"Perils":"S",
	"CutOffDate":"2020-12-30",
	"PortfolioType":1,
	"Portfolios":["/home/hiar/SwissRe/r-core/EQ_Ind.xml"],
	"ResultsPath":"/home/hiar/SwissRe/r-core/results",
	"SystemPath":"/home/hiar/SwissRe/r-core/miniR_fs"
}

miniR

```sh
#In each execution the process type must be changed in the configuration file
#ProcessType = L
dotnet "miniR.dll" "/home/hiar/SwissRe/miniR/cfg_eq.json" 1 1 

#ProcessType = LM this process nust be alive
dotnet "miniR.dll" "/home/hiar/SwissRe/miniR/cfg_eq.json" 1 1 

#ProcessType = LC
dotnet "miniR.dll" "/home/hiar/SwissRe/miniR/cfg_eq.json" 1 2
dotnet "miniR.dll" "/home/hiar/SwissRe/miniR/cfg_eq.json" 2 2

#ProcessType = LS
dotnet "miniR.dll" "/home/hiar/SwissRe/miniR/cfg_eq.json" 1 2

# WE MUST KILL "LM" PROCESS


```

RH-Mex

```sh
#In each execution the process type must be changed in the configuration file

#ProcessType = L
dotnet "RH-Mex_core.dll" "/home/hiar/SwissRe/miniR/cfg_t1.json" 1 1 

#ProcessType = LC
dotnet "RH-Mex_core.dll" "/home/hiar/SwissRe/miniR/cfg_t1.json" 1 2 
dotnet "RH-Mex_core.dll" "/home/hiar/SwissRe/miniR/cfg_t1.json" 2 2 

#ProcessType = LS
dotnet "RH-Mex_core.dll" "/home/hiar/SwissRe/miniR/cfg_t1.json" 1 2 
```
