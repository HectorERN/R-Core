# miniR

This system is based on the version of the System R Plus (desktop) for its execution through a series of parameters through a console or terminal. 

In the following links you can find a compressed files which contains a folder with all the files necessary for its execution. 

This repository describes the syntax of the parameters to be used and a couple of examples are added to test the functionality.

## Links
miniR (2 MB) [download](https://serv.ern.com.mx/download/SwissRe_PATM/miniR.zip)

miniR File System (630 MB) [download](https://serv.ern.com.mx/download/SwissRe_PATM/miniR_fs.zip)

## Sintaxis miniR
Argument definition

|Field|Available Values|Comments|
|---|---|---|
|File System (fs)|"{path}"|File System Path| 
|Process|L, LC, LS|L=Load Portfolio, LC=Load and Compute, LS=Load and Accumulate|
|Initial Chunk|numeric|1| 
|Total Chunks|numeric|4| 
|Peril|S, H, T, SR|S=Earthquake| 
|Cut of Date|yyyy-MM-dd|2020-10-27|
|PortfolioTyoe|1, 2, 3|1=Individual,2=Collective,3=Both|
|Results Path|"{path}"|"D:\Ejemplos\PATM\resultados"|
|Portfolio|"{file}"|"D:\Ejemplos\PATM\Independiente_SISMO.xml"|
|---|---|---|

dotnet "miniR.dll" "[FS]" [Process] [iniChunk] [totChunks] [Peril] [CutOfDate] [PortfolioTyoe] "[ResultsPath]" "[Portfolio]"

### Example

Load Portolio
```sh
dotnet "miniR.dll" "/home/hiar/SwissRe/miniR/miniR_fs" L 1 1 S 2020-10-20 1 "/home/hiar/SwissRe/miniR/Tests" "/home/hiar/SwissRe/miniR/Portfolios/testSismo_TC.xml"
```

Load Portolio (binary file) and Compute Chunk
```sh
dotnet "miniR.dll" "/home/hiar/SwissRe/miniR/miniR_fs" L 1 1 S 2020-10-20 1 "/home/hiar/SwissRe/miniR/Tests" "/home/hiar/SwissRe/miniR/Portfolios/testSismo_TC.xml"
```

Accumulate Chunks
```sh
dotnet "miniR.dll" "/home/hiar/SwissRe/miniR/miniR_fs" L 1 1 S 2020-10-20 1 "/home/hiar/SwissRe/miniR/Tests" "/home/hiar/SwissRe/miniR/Portfolios/testSismo_TC.xml"
```