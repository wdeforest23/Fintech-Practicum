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
Combined_Data_Success_Dummies <- Combined_Data_Success_Dummies %>% mutate(standard_Total_Capital_Raised = (Total_Capital_Raised - mean(Total_Capital_Raised))/sd(Total_Capital_Raised), standard_Product_Market_Fit = (Product_Market_Fit - mean(Product_Market_Fit))/sd(Product_Market_Fit), standard_Total_Financing_Rounds = (Total_Financing_Rounds - mean(Total_Financing_Rounds))/sd(Total_Financing_Rounds), standard_Liquidity_Event_Reached = (Liquidity_Event_Reached - mean(Liquidity_Event_Reached))/sd(Liquidity_Event_Reached), standard_length_of_company_life = (length_of_company_life - mean(length_of_company_life, na.rm=TRUE))/sd(length_of_company_life, na.rm=TRUE), standard_Total_Top_VCs = (Total_Top_VCs - mean(Total_Top_VCs))/sd(Total_Top_VCs))

Combined_Data_Success_Dummies <- Combined_Data_Success_Dummies %>% group_by(Company) %>% mutate(Combined_Success_Measure = sum(standard_Total_Capital_Raised, standard_Product_Market_Fit, standard_Total_Financing_Rounds, standard_Liquidity_Event_Reached, standard_length_of_company_life, standard_Total_Top_VCs, na.rm=TRUE))
```

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
#summary statistics

CMC_Obs <- Combined_Data_Success_Dummies %>% filter(CMC_Dummy == "1")
CMC_econ <- CMC_Obs %>% group_by(economics_dummy) %>% summarize(n=n()) %>% mutate(prop=n/sum(n))
CMC_econ
```

    ## # A tibble: 2 x 3
    ##   economics_dummy     n  prop
    ##             <dbl> <int> <dbl>
    ## 1               0    61 0.415
    ## 2               1    86 0.585

``` r
CMC_gender <- CMC_Obs %>% group_by(gender) %>% summarize(n=n()) %>% mutate(prop=n/sum(n))
CMC_gender
```

    ## # A tibble: 3 x 3
    ##   gender     n  prop
    ##   <chr>  <int> <dbl>
    ## 1 -         16 0.109
    ## 2 female    15 0.102
    ## 3 male     116 0.789

``` r
Pomona_Obs <- Combined_Data_Success_Dummies %>% filter(Pomona_Dummy == "1") %>% head()

Pitzer_Obs <- Combined_Data_Success_Dummies %>% filter(Pitzer_Dummy == "1") %>% head()

Scripps_Obs <- Combined_Data_Success_Dummies %>% filter(Scripps_Dummy == "1") %>% head()

HMC_Obs <- Combined_Data_Success_Dummies %>% filter(HMC_Dummy == "1") %>% head()

Summary_7C <- Combined_Data_Success_Dummies %>% rename("School_Affiliations_of_Founders"= 'School Affiliations of Founders') %>% group_by(School_Affiliations_of_Founders) %>% summarize(n=n()) %>% mutate(prop=n/sum(n), total=sum(n))
Summary_7C
```

    ## # A tibble: 19 x 4
    ##    School_Affiliations_of_Founders     n    prop total
    ##    <chr>                           <int>   <dbl> <int>
    ##  1 CGU                                63 0.0775    813
    ##  2 CGU,CMC                             1 0.00123   813
    ##  3 CGU,PI                              3 0.00369   813
    ##  4 CMC                               153 0.188     813
    ##  5 CMC,CGU                             1 0.00123   813
    ##  6 CMC,Keck                            2 0.00246   813
    ##  7 CMC,PO                              2 0.00246   813
    ##  8 HMC                               175 0.215     813
    ##  9 HMC,CGU                             1 0.00123   813
    ## 10 HMC,CMC                             3 0.00369   813
    ## 11 HMC,PO                              1 0.00123   813
    ## 12 Keck                               32 0.0394    813
    ## 13 PI                                 77 0.0947    813
    ## 14 PI,CGU                              1 0.00123   813
    ## 15 PI,HMC                              1 0.00123   813
    ## 16 PO                                273 0.336     813
    ## 17 PO,CGU                              1 0.00123   813
    ## 18 PO,HMC                              2 0.00246   813
    ## 19 SC                                 21 0.0258    813

``` r
#Standardized Success variable distributions
library(dplyr)
library(ggplot2)

dist_total_capital_raised <- ggplot(data=Combined_Data_Success_Dummies, aes(x=standard_Total_Capital_Raised)) + geom_density()
dist_total_capital_raised
```

![](Dataset-creation-using-Excel_files/figure-gfm/unnamed-chunk-11-1.png)<!-- -->

``` r
dist_Product_Market_Fit <- ggplot(data=Combined_Data_Success_Dummies, aes(x=standard_Product_Market_Fit)) + geom_density()
dist_Product_Market_Fit
```

![](Dataset-creation-using-Excel_files/figure-gfm/unnamed-chunk-11-2.png)<!-- -->

``` r
dist_Total_Financing_Rounds <- ggplot(data=Combined_Data_Success_Dummies, aes(x=standard_Total_Financing_Rounds)) + geom_density()
dist_Total_Financing_Rounds
```

![](Dataset-creation-using-Excel_files/figure-gfm/unnamed-chunk-11-3.png)<!-- -->

``` r
dist_Liquidity_Event_Reached <- ggplot(data=Combined_Data_Success_Dummies, aes(x=standard_Liquidity_Event_Reached)) + geom_density()
dist_Liquidity_Event_Reached
```

![](Dataset-creation-using-Excel_files/figure-gfm/unnamed-chunk-11-4.png)<!-- -->

``` r
dist_length_of_company_life <- ggplot(data=Combined_Data_Success_Dummies, aes(x=standard_length_of_company_life)) + geom_density()
dist_length_of_company_life
```

    ## Warning: Removed 29 rows containing non-finite values (stat_density).

![](Dataset-creation-using-Excel_files/figure-gfm/unnamed-chunk-11-5.png)<!-- -->

``` r
dist_Total_Top_VCs <- ggplot(data=Combined_Data_Success_Dummies, aes(x=standard_Total_Top_VCs)) + geom_density()
dist_Total_Top_VCs
```

![](Dataset-creation-using-Excel_files/figure-gfm/unnamed-chunk-11-6.png)<!-- -->

``` r
dist_Combined_Success_Measure <- ggplot(data=Combined_Data_Success_Dummies, aes(x=Combined_Success_Measure)) + geom_density()
dist_Combined_Success_Measure
```

![](Dataset-creation-using-Excel_files/figure-gfm/unnamed-chunk-11-7.png)<!-- -->
