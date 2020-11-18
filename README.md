# miniR

This system is based on the version of the System R Plus (desktop) for its execution through a series of parameters through a console or terminal. 

In the following links you can find a compressed files which contains a folder with all the files necessary for its execution. 

This repository describes the syntax of the parameters to be used and a couple of examples are added to test the functionality.

## Links
miniR (2 MB) [download](https://serv.ern.com.mx/download/SwissRe_PATM/miniR.zip) (updated 2020-11-18)

miniR File System (465 MB) [download](https://serv.ern.com.mx/download/SwissRe_PATM/miniR_fs.zip) (updated 2020-11-10)

## Sintaxis miniR
Argument definition

|Field|Available Values|Comments|
|---|---|---|
|File System (FS)|"{path}"|File System Path "/home/hiar/SwissRe/miniR/miniR_fs"| 
|Process|L, LC, LS|L=Load Portfolio, LC=Load and Compute, LS=Load and Accumulate|
|Initial Chunk|numeric|1| 
|Total Chunks|numeric|4| 
|Peril|S, SR|S=Earthquake, SR=Earthquake (Regulatory)| 
|Cut of Date|yyyy-MM-dd|2020-10-27|
|PortfolioType|1, 2, 3|1=Individual,2=Collective,3=Both|
|Results Path|"{path}"|"/home/hiar/SwissRe/miniR/Tests"|
|Portfolio|"{file}"|"/home/hiar/SwissRe/miniR/Portfolios/EQ_Ind.xml"|
|PortfolioCollective*|"{file}"|"/home/hiar/SwissRe/miniR/Portfolios/EQ_Col.xml"|
|---|---|---|



* *The last parameter (Portfolio Collective) is added only in case PortfolioType 3 has been selected.


PortolioType (1 or 2)

* dotnet "miniR.dll" "[FS]" [Process] [iniChunk] [totChunks] [Peril] [CutOfDate] [PortfolioTyoe] "[ResultsPath]" "[Portfolio]"

PortolioType (3)

* dotnet "miniR.dll" "[FS]" [Process] [iniChunk] [totChunks] [Peril] [CutOfDate] [PortfolioTyoe] "[ResultsPath]" "[Portfolio]" "[PortfolioCollective]"


## Examples

### Example 1 (Individual)

PortfolioType = 1

```sh
dotnet "miniR.dll" "/home/hiar/SwissRe/miniR/miniR_fs" L 1 1 S 2020-10-20 1 "/home/hiar/SwissRe/miniR/Tests" "/home/hiar/SwissRe/miniR/Portfolios/EQ_Ind.xml"
dotnet "miniR.dll" "/home/hiar/SwissRe/miniR/miniR_fs" LC 1 1 S 2020-10-20 1 "/home/hiar/SwissRe/miniR/Tests" "/home/hiar/SwissRe/miniR/Portfolios/EQ_Ind.xml"
dotnet "miniR.dll" "/home/hiar/SwissRe/miniR/miniR_fs" LS 1 1 S 2020-10-20 1 "/home/hiar/SwissRe/miniR/Tests" "/home/hiar/SwissRe/miniR/Portfolios/EQ_Ind.xml"
```

### Example 2 (Collective)

PortfolioType = 2

```sh
dotnet "miniR.dll" "/home/hiar/SwissRe/miniR/miniR_fs" L 1 1 S 2020-10-20 2 "/home/hiar/SwissRe/miniR/Tests" "/home/hiar/SwissRe/miniR/Portfolios/EQ_Col.xml"
dotnet "miniR.dll" "/home/hiar/SwissRe/miniR/miniR_fs" LC 1 1 S 2020-10-20 2 "/home/hiar/SwissRe/miniR/Tests" "/home/hiar/SwissRe/miniR/Portfolios/EQ_Col.xml"
dotnet "miniR.dll" "/home/hiar/SwissRe/miniR/miniR_fs" LS 1 1 S 2020-10-20 2 "/home/hiar/SwissRe/miniR/Tests" "/home/hiar/SwissRe/miniR/Portfolios/EQ_Col.xml"
```

### Example 3 (Individual and Collective)

PortfolioType = 3 (tha last parameter [PortfolioCollective] is included)

```sh
dotnet "miniR.dll" "/home/hiar/SwissRe/miniR/miniR_fs" L 1 1 S 2020-10-20 3 "/home/hiar/SwissRe/miniR/Tests" "/home/hiar/SwissRe/miniR/Portfolios/EQ_Ind.xml" "/home/hiar/SwissRe/miniR/Portfolios/EQ_Col.xml"
dotnet "miniR.dll" "/home/hiar/SwissRe/miniR/miniR_fs" LC 1 1 S 2020-10-20 3 "/home/hiar/SwissRe/miniR/Tests" "/home/hiar/SwissRe/miniR/Portfolios/EQ_Ind.xml" "/home/hiar/SwissRe/miniR/Portfolios/EQ_Col.xml"
dotnet "miniR.dll" "/home/hiar/SwissRe/miniR/miniR_fs" LS 1 1 S 2020-10-20 3 "/home/hiar/SwissRe/miniR/Tests" "/home/hiar/SwissRe/miniR/Portfolios/EQ_Ind.xml" "/home/hiar/SwissRe/miniR/Portfolios/EQ_Col.xml"
```

### Example 3 (Regulatory Assestment)

Peril = SR

```sh
dotnet "miniR.dll" "/home/hiar/SwissRe/miniR/miniR_fs" L 1 1 SR 2020-10-20 1 "/home/hiar/SwissRe/miniR/Tests" "/home/hiar/SwissRe/miniR/Portfolios/EQ_Ind.xml"
dotnet "miniR.dll" "/home/hiar/SwissRe/miniR/miniR_fs" LC 1 1 SR 2020-10-20 1 "/home/hiar/SwissRe/miniR/Tests" "/home/hiar/SwissRe/miniR/Portfolios/EQ_Ind.xml"
dotnet "miniR.dll" "/home/hiar/SwissRe/miniR/miniR_fs" LS 1 1 SR 2020-10-20 1 "/home/hiar/SwissRe/miniR/Tests" "/home/hiar/SwissRe/miniR/Portfolios/EQ_Ind.xml"
```
