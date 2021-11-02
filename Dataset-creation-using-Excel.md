Data Wrangling
================
William DeForest, Nate Coffin, Ethan Dieck, Samantha Manywa
11/1/2021

**Dataset creation using Excel**

``` r
library(readxl)
AirTables_Data <- read_excel("C:\\Users\\wdd72\\OneDrive\\Documents\\Junior Fall\\Fintech Practicum\\Fintech_Data\\Companies-Fintech Practicum View.xlsx")
Unique_Obs <- read_excel("C:\\Users\\wdd72\\OneDrive\\Documents\\Junior Fall\\Fintech Practicum\\Fintech_Data\\Unique_Company_Founder_Obs.xlsx")
PDL_Data <- read_excel("C:\\Users\\wdd72\\OneDrive\\Documents\\Junior Fall\\Fintech Practicum\\Fintech_Data\\Final Clean PDL Data.xlsx")
```

    ## New names:
    ## * industry -> industry...8
    ## * name -> name...20
    ## * size -> size...21
    ## * id -> id...22
    ## * founded -> founded...23
    ## * ...

``` r
DummyVars <- read_excel("C:\\Users\\wdd72\\OneDrive\\Documents\\Junior Fall\\Fintech Practicum\\Fintech_Data\\Dummy Variables 10.7.21.xlsx")
Success_Measures <- read_excel("C:\\Users\\wdd72\\OneDrive\\Documents\\Junior Fall\\Fintech Practicum\\Fintech_Data\\Success Measures.xlsx")
```

``` r
library(dplyr)
```

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
Unique_Obs$founders_lower <- tolower(Unique_Obs$Founders)
Unique_Obs_PDL <- left_join(Unique_Obs, PDL_Data, by=c("founders_lower"="full_name"))
Unique_Obs_PDL
```

    ## # A tibble: 813 x 586
    ##    Company             Founders        founders_lower  gender birth_year linkedin_userna~
    ##    <chr>               <chr>           <chr>           <chr>  <chr>                 <dbl>
    ##  1 BeSababa            Aaron Wazana    aaron wazana    male   -                         1
    ##  2 54genevels          Abasi Ene-Obong abasi ene-obong male   -                         1
    ##  3 Traffic Marketplace Adam Altman     adam altman     male   1977                      1
    ##  4 SMNI                Adam Altman     adam altman     male   1977                      1
    ##  5 Rebilly             Adam Altman     adam altman     male   1977                      1
    ##  6 Redocly             Adam Altman     adam altman     male   1977                      1
    ##  7 PAX Labs            Adam Bowen      adam bowen      male   -                         1
    ##  8 Juul                Adam Bowen      adam bowen      male   -                         1
    ##  9 Comprisma           Adam Pelavin    adam pelavin    male   -                         1
    ## 10 Cheddr Media        Adam Schoenfeld adam schoenfeld male   -                         1
    ## # ... with 803 more rows, and 580 more variables: facebook_username <dbl>,
    ## #   twitter_username <dbl>, github_username <dbl>, industry...8 <chr>,
    ## #   job_title <chr>, job_title_role <chr>, job_title_sub_role <chr>,
    ## #   job_title_levels <chr>, job_company_name <chr>, job_company_size <chr>,
    ## #   job_company_founded <chr>, job_company_industry <chr>,
    ## #   job_company_location_name <chr>, job_last_updated <dttm>,
    ## #   job_start_date <chr>, name...20 <chr>, size...21 <chr>, id...22 <chr>, ...

``` r
Combined_Data <- left_join(Unique_Obs_PDL, AirTables_Data, by=c("Company"="Name"))
Combined_Data
```

    ## # A tibble: 813 x 703
    ##    Company             Founders.x      founders_lower  gender birth_year linkedin_userna~
    ##    <chr>               <chr>           <chr>           <chr>  <chr>                 <dbl>
    ##  1 BeSababa            Aaron Wazana    aaron wazana    male   -                         1
    ##  2 54genevels          Abasi Ene-Obong abasi ene-obong male   -                         1
    ##  3 Traffic Marketplace Adam Altman     adam altman     male   1977                      1
    ##  4 SMNI                Adam Altman     adam altman     male   1977                      1
    ##  5 Rebilly             Adam Altman     adam altman     male   1977                      1
    ##  6 Redocly             Adam Altman     adam altman     male   1977                      1
    ##  7 PAX Labs            Adam Bowen      adam bowen      male   -                         1
    ##  8 Juul                Adam Bowen      adam bowen      male   -                         1
    ##  9 Comprisma           Adam Pelavin    adam pelavin    male   -                         1
    ## 10 Cheddr Media        Adam Schoenfeld adam schoenfeld male   -                         1
    ## # ... with 803 more rows, and 697 more variables: facebook_username <dbl>,
    ## #   twitter_username <dbl>, github_username <dbl>, industry...8 <chr>,
    ## #   job_title <chr>, job_title_role <chr>, job_title_sub_role <chr>,
    ## #   job_title_levels <chr>, job_company_name <chr>, job_company_size <chr>,
    ## #   job_company_founded <chr>, job_company_industry <chr>,
    ## #   job_company_location_name <chr>, job_last_updated <dttm>,
    ## #   job_start_date <chr>, name...20 <chr>, size...21 <chr>, id...22 <chr>, ...

``` r
library(dplyr)
Combo_Dummys <- left_join(Combined_Data, DummyVars, by=c("founders_lower"="FOUNDER"))
Combo_Dummys
```

    ## # A tibble: 813 x 890
    ##    Company             Founders.x      founders_lower  gender birth_year linkedin_userna~
    ##    <chr>               <chr>           <chr>           <chr>  <chr>                 <dbl>
    ##  1 BeSababa            Aaron Wazana    aaron wazana    male   -                         1
    ##  2 54genevels          Abasi Ene-Obong abasi ene-obong male   -                         1
    ##  3 Traffic Marketplace Adam Altman     adam altman     male   1977                      1
    ##  4 SMNI                Adam Altman     adam altman     male   1977                      1
    ##  5 Rebilly             Adam Altman     adam altman     male   1977                      1
    ##  6 Redocly             Adam Altman     adam altman     male   1977                      1
    ##  7 PAX Labs            Adam Bowen      adam bowen      male   -                         1
    ##  8 Juul                Adam Bowen      adam bowen      male   -                         1
    ##  9 Comprisma           Adam Pelavin    adam pelavin    male   -                         1
    ## 10 Cheddr Media        Adam Schoenfeld adam schoenfeld male   -                         1
    ## # ... with 803 more rows, and 884 more variables: facebook_username <dbl>,
    ## #   twitter_username <dbl>, github_username <dbl>, industry...8 <chr>,
    ## #   job_title <chr>, job_title_role <chr>, job_title_sub_role <chr>,
    ## #   job_title_levels <chr>, job_company_name <chr>, job_company_size <chr>,
    ## #   job_company_founded <chr>, job_company_industry <chr>,
    ## #   job_company_location_name <chr>, job_last_updated <dttm>,
    ## #   job_start_date <chr>, name...20 <chr>, size...21 <chr>, id...22 <chr>, ...

``` r
library(dplyr)
Combined_Data_Success_Dummies <- left_join(Combo_Dummys, Success_Measures, by=c("Company"="Company", "Founders.x"="Founders"))
Combined_Data_Success_Dummies
```

    ## # A tibble: 813 x 897
    ##    Company             Founders.x      founders_lower  gender birth_year linkedin_userna~
    ##    <chr>               <chr>           <chr>           <chr>  <chr>                 <dbl>
    ##  1 BeSababa            Aaron Wazana    aaron wazana    male   -                         1
    ##  2 54genevels          Abasi Ene-Obong abasi ene-obong male   -                         1
    ##  3 Traffic Marketplace Adam Altman     adam altman     male   1977                      1
    ##  4 SMNI                Adam Altman     adam altman     male   1977                      1
    ##  5 Rebilly             Adam Altman     adam altman     male   1977                      1
    ##  6 Redocly             Adam Altman     adam altman     male   1977                      1
    ##  7 PAX Labs            Adam Bowen      adam bowen      male   -                         1
    ##  8 Juul                Adam Bowen      adam bowen      male   -                         1
    ##  9 Comprisma           Adam Pelavin    adam pelavin    male   -                         1
    ## 10 Cheddr Media        Adam Schoenfeld adam schoenfeld male   -                         1
    ## # ... with 803 more rows, and 891 more variables: facebook_username <dbl>,
    ## #   twitter_username <dbl>, github_username <dbl>, industry...8 <chr>,
    ## #   job_title <chr>, job_title_role <chr>, job_title_sub_role <chr>,
    ## #   job_title_levels <chr>, job_company_name <chr>, job_company_size <chr>,
    ## #   job_company_founded <chr>, job_company_industry <chr>,
    ## #   job_company_location_name <chr>, job_last_updated <dttm>,
    ## #   job_start_date <chr>, name...20 <chr>, size...21 <chr>, id...22 <chr>, ...

``` r
write.csv(Combined_Data,"C:\\Users\\wdd72\\OneDrive\\Documents\\Junior Fall\\Fintech Practicum\\Fintech_Data\\Master_Combined_Data.csv", row.names = FALSE)
```

``` r
write.csv(Combo_Dummys,"C:\\Users\\wdd72\\OneDrive\\Documents\\Junior Fall\\Fintech Practicum\\Fintech_Data\\Combined_with_Dummies.csv", row.names = FALSE)
```

``` r
write.csv(Unique_Obs_PDL,"C:\\Users\\wdd72\\OneDrive\\Documents\\Junior Fall\\Fintech Practicum\\Fintech_Data\\Unique_Obs_PDL.csv", row.names = FALSE)
```

``` r
write.csv(Combined_Data_Success_Dummies,"C:\\Users\\wdd72\\OneDrive\\Documents\\Junior Fall\\Fintech Practicum\\Fintech_Data\\Combined_Data_For_Regression.csv", row.names = FALSE)
```

``` r
library(dplyr)
regression <- lm(Total_Financing_Rounds ~ Pitzer_Dummy +    HMC_Dummy   + CMC_Dummy +   Scripps_Dummy + Pomona_Dummy, data = Combined_Data_Success_Dummies)
print(regression)
```

    ## 
    ## Call:
    ## lm(formula = Total_Financing_Rounds ~ Pitzer_Dummy + HMC_Dummy + 
    ##     CMC_Dummy + Scripps_Dummy + Pomona_Dummy, data = Combined_Data_Success_Dummies)
    ## 
    ## Coefficients:
    ##   (Intercept)   Pitzer_Dummy      HMC_Dummy      CMC_Dummy  Scripps_Dummy  
    ##       0.16214       -0.05446        0.02014        0.13495       -0.07332  
    ##  Pomona_Dummy  
    ##       0.15060
