# Portfolios


The system currently has the capability to support a variety of formats this installation supports a CSV files with the OED standard.

# OED

For a detailed description of the OED file format, please refer to the official documentation via the following links:

|Description|Link|
|---|---|
|Github Repository |[GitHub](https://github.com/OasisLMF/OpenDataStandards)|
|OED Specification| [Specification](https://github.com/OasisLMF/OpenDataStandards/blob/master/OpenExposureData/Docs/OpenExposureData_Spec.xlsx)|
|OED Documentation | [Overview](https://github.com/OasisLMF/OpenDataStandards/tree/master/OpenExposureData)
|Reinsurance Detailed | [Reinsurance](https://github.com/OasisLMF/OpenDataStandards/blob/master/OpenExposureData/7_OED_Reinsurance.rst)



# Secondary modifiers - FlexiLoc Catalogs

Since ERN implements secondary modifiers currently not supported in the OED standard, the following fields were added to the FlexiLoc catalogue:

---

* FlexiLocShortColumn
  
|Description|Value|
|---|---|
|HasShortColumns|1|
|NoShortColumns|0|
<br>

* FlexiLocPosibilityOfPounding	
  
|Description|Value|
|---|---|
|With lower buildings|1|
|With buildings of equal or greater height|2|
|With lower and higher buildings|3|
|No possibility of knocking|4|
<br>
* FlexiLocPreviousDamage	

|Description|Value|
|---|---|
|Property with previous damage|1|
|Property without previous damage|0|
<br>
* FlexiLocIrregularitiesInPlant	
  
|Description|Value|
|---|---|
|Irregularity null|1|
|Little irregularity|2|
|High irregularity|3|
<br>
* FlexiLocCorner	
  
|Description|Value|
|---|---|
|Property located on a corner|1|
|Not located on a corner|0|
<br>

* FlexiLocRepaired	
  
|Description|Value|
|---|---|
|Yes, they were repaired|1|
|Not repaired|0|
<br>

* FlexiLocIrregularitiesInElevation	
  
|Description|Value|
|---|---|
|Irregularity null|1|
|Little irregularity|2|
|High irregularity|3|
<br>
* FlexiLocStory	
  
|Description|Value|
|---|---|
|Numeric| 1 - 57|
<br>
* FlexiLocOverweight	
  
|Description|Value|
|---|---|
|Is overweight|1|
|Not overweight|0|

* FlexiLocBeachFront
  
|Description|Value|
|---|---|
|Is on beach front|1|
|Not in beach front |0|


* FlexiLocSoftStory
  
|Description|Value|
|---|---|
|Has Soft Story|1|
|Not Soft Story|0|

<br>

#  Results

The application generates different types of results (in csv format), either by location, by hazard, by peril and by portfolio, such as Premiums (AAL), ELTs, PML curves, as well as the results of the implementation of reinsurance contracts.

<br>

## Premiums

    The files show the Average Annual Losses.

Scope
  * Hazard & Peril
  * Location
  * Accumulated by grouping zones (or Cresta Zones)

<br>

### Hazard & Perils

This file in csv format contains 5 columns and each row will correspond to each evaluated hazard.

|Field|Description|
|---|---|
|Peril|Peril code|
|GroundUpLoss|Ground Up Loss|
|GrossLoss|Gross Loss|
|NetLoss(Pre-CAT)|Net Retained Loss before CAT|
|CededLoss|Ceded Loss|

Example
|Peril|GrossLoss|NetLoss (Pre-CAT)|GroundUpLoss|CededLoss|
|---|---|---|---|---|
|QEQ|10000.00|7000.00|12000.00|3000.00|
|WW1|10000.00|7000.00|12000.00|3000.00|

<br>

---
### Location

<br>
This file contains the premium result for each Peril - Financial Perspective - Location. Initially the system displays the Ground Up, Gross and Retained (Pre-CAT) results and if reinsurance information is entered it will display the Ceded, Quota Shared, Gross No Facultative and Surplus perspectives depending on the information entered.

<br>

Example

|LocID|QEQ_GroundUp|QEQ_Gross|QEQ_GrossNoF|QEQ_Retained_PreCAT|QEQ_Ceded|QEQ_CededQS|QEQ_Ceded_SS|
|--|---|---|---|---|---|---|---|
|1|62.02399181|62.02399181|62.02399181|31.01199591|31.01199591|24.80959673|6.20239917|
|2|49.39311307|49.39311307|49.39311307|24.69655653|24.69655653|19.75724522|4.93931132|

---
<br>

### Accumulated by Grooping Zones

This file contains the premium result for each Peril - Financial Perspective aggregated by zone. Initially the system displays the Ground Up, Gross and Retained (Pre-CAT) results and if reinsurance information is entered it will display the Ceded, Quota Shared, Gross No Facultative and Surplus perspectives depending on the information entered.

|ZONE|QEQ_GroundUp|QEQ_Gross|QEQ_Retained_PreCAT|QEQ_Ceded|
|---|---|---|---|---|
|ZONA_1|62.02399181|62.02399181|31.01199591|31.01199591|
|ZONA_2|49.39311307|49.39311307|24.69655653|24.69655653|

---
## Event Loss Table (ELT)

They contain the information of the Loss Distribution Function (LDF) for each source which is a truncated BETA, the parameters of this LDF are the Expected Value of Loss (EP), the Variance of Loss (VAR) and the truncations by effect of the Deductible (PP0) and by the limit (PP1).

Scope
  * Hazard & Peril
  
|Field|Description|
|---|---|
|TMP|Denote to which peril each record in the loss file is related.| 
|ESC|Describe the scenario number. It is a value derived by concatenating the prefix "ESC00" and the scenario number evaluated.|
|Frec|Frequency, i.e. the probability of annual occurrence of an event.|
|E(P)|This column represents the expected value of the loss (it is an average value).|
|S(P)|This column represents the standard deviation of the loss (dispersion).|
|a|Represents one of the parameters that are considered in the Beta distribution.|
|b|Represents another of the parameters that are considered in the Beta distribution.|
|P0|Represents the truncation of the FDP due to the effect of the deductible.|
|P1|Represents the truncation of the WTP due to the effect of the limit.|
|Exp|Is the value of the exposed, i.e. the value of the maximum loss.|
|SSigma|Sum of the standard deviations of all the locations evaluated without considering correlation.|
|SVar|Sum of the variances of all the locations without considering correlation.|
|Scenario Description|This column is informative and contains the name of the event and a brief description.|

---
## Results by Scenario Evaluation

When evaluating a specific scenario, the system will generate two types of results, Premiums and Losses per location and per peril.
  * Result by Peril
  
|Peril|GrossLoss|NetLoss(Pre-CAT)|GroundUp|Ceded|
|---|---|---|---|---|
|QEQ|126891.50|63445.75|139580.65|63445.75|

  * Result by Location

|LocID|QEQ_Gross|QEQ_Net(Pre-CAT)|QEQ_GroundUp|QEQ_Ceeded|
|---|---|---|---|---|
|1|144296.36|0|144296.36|144296.36|
|2|168920.39|0|168920.39|168920.39|