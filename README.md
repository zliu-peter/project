# Project: week 6-7 HW (Stata II)

## Objective

The purpose of this study is to explore the importance of "self-reported health" as a health indicator, suing publicly available datasets. It is part of the week 6-7 HW for STATA Intermediate course. The week 6's focus is on documentation and website creation, while the week 7's focus is on visualizations.

## Data Source

There are two main data source, with instructions for access.

+ NHANES Survey Data
  - Dated 1999-2000
  ```stata
  import sasxport5 "https://wwwn.cdc.gov/Nchs/Nhanes/1999-2000/DEMO.XPT", clear
  ```

+ NCHS (20-year period) Mortality Follow-up Data
  - Click this [link](https://ftp.cdc.gov/pub/), and follow the instructions as followed:
  - Health Statistics
    - NCHS
      - datalinkage
        - Linked Mortality
          - ```NHANES_1999_2000_MORT_2019_PUBLIC.dat```
  
+ Code for Data Aquisition in STATA          
   ```stata
    //data
     global mort_1999_2000 https://ftp.cdc.gov/pub/HEALTH_STATISTICS/NCHS/datalinkage/linked_mortality/NHANES_1999_2000_MORT_2019_PUBLIC.dat

     //code
      cat https://ftp.cdc.gov/pub/HEALTH_STATISTICS/NCHS/datalinkage/linked_mortality/Stata_ReadInProgramAllSurveys.do
   ```

## Code Protocols
+ Access the data file from NCHS as specified above
  - Make sure this [file](https://ftp.cdc.gov/pub/HEALTH_STATISTICS/NCHS/datalinkage/linked_mortality/NHANES_1999_2000_MORT_2019_PUBLIC.dat) is downloaded either from this website or from my repo

+ Edit the `SURVEY` and alter it to `NHANES_1999_2000`

+ Edit the directory and save the file as `followup.do`

+ Merging survey and mortality data with the following code
  
  ```stata
  //use your own username/project repo instead of the class repo below
  global repo "https://github.com/zliu-peter/project/raw/main/"
  do ${repo}followup.do
  save followup, replace
  ```

+ Merge datasets
  ```stata
  import sasxport5 "https://wwwn.cdc.gov/Nchs/Nhanes/1999-2000/DEMO.XPT", clear
  merge 1:1 seqn using followup
  lookfor follow
  ```

## Week 7 analysis

+ Inference
  - Employ 95% CI and p-values basis
  ```stata
  merge 1:1 seqn using demo_mortality, nogen
  sts graph, by(huq010) fail
  stcox i.huq010
  ```
  - Brief conclusion basis
  ```stata
  import sasxport5 "https://wwwn.cdc.gov/Nchs/Nhanes/1999-2000/HUQ.XPT", clear 
  huq010 
  desc huq010
  codebook huq010
  ```
+ Results and plots (week 7).
Click [here](dyndoc.html) to view nonparametric and semiparametric risk estimates from Stata
