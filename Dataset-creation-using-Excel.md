Data Wrangling
================
William DeForest, Nate Coffin, Ethan Dieck, Samantha Manywa
11/1/2021

**Dataset creation using Excel**

``` r
#load packages
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
library(tidyr)
library(tidyverse)
```

    ## -- Attaching packages --------------------------------------- tidyverse 1.3.1 --

    ## v ggplot2 3.3.5     v purrr   0.3.4
    ## v tibble  3.1.4     v stringr 1.4.0
    ## v readr   2.0.2     v forcats 0.5.1

    ## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(readxl)
library(ggplot2)
```

``` r
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
ConcatData <- read_excel("C:\\Users\\wdd72\\OneDrive\\Documents\\Junior Fall\\Fintech Practicum\\Fintech_Data\\Concatenated_Vars.xlsx")
```

    ## New names:
    ## * name -> name...1
    ## * industry...8 -> industry...9
    ## * name...20 -> name...21
    ## * size...21 -> size...22
    ## * id...22 -> id...23
    ## * ...

``` r
Success_Measures <- read_excel("C:\\Users\\wdd72\\OneDrive\\Documents\\Junior Fall\\Fintech Practicum\\Fintech_Data\\Success Measures.xlsx")
```

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
ConcatVars <- ConcatData %>% select(name...1, Company, company:major)
Combo_Dummy_Concat <- left_join(Combo_Dummys, ConcatVars, by=c("founders_lower"="name...1", "Company"="Company"))
```

``` r
Combined_Data_Success_Dummies <- left_join(Combo_Dummy_Concat, Success_Measures, by=c("Company"="Company", "Founders.x"="Founders"))
Combined_Data_Success_Dummies <- Combined_Data_Success_Dummies %>% mutate(standard_Total_Capital_Raised = (Total_Capital_Raised - mean(Total_Capital_Raised))/sd(Total_Capital_Raised), standard_Product_Market_Fit = (Product_Market_Fit - mean(Product_Market_Fit))/sd(Product_Market_Fit), standard_Total_Financing_Rounds = (Total_Financing_Rounds - mean(Total_Financing_Rounds))/sd(Total_Financing_Rounds), standard_Liquidity_Event_Reached = (Liquidity_Event_Reached - mean(Liquidity_Event_Reached))/sd(Liquidity_Event_Reached), standard_length_of_company_life = (length_of_company_life - mean(length_of_company_life, na.rm=TRUE))/sd(length_of_company_life, na.rm=TRUE), standard_Total_Top_VCs = (Total_Top_VCs - mean(Total_Top_VCs))/sd(Total_Top_VCs))

Combined_Data_Success_Dummies <- Combined_Data_Success_Dummies %>% group_by(Company) %>% mutate(Combined_Success_Measure = sum(standard_Total_Capital_Raised, standard_Product_Market_Fit, standard_Total_Financing_Rounds, standard_Liquidity_Event_Reached, standard_length_of_company_life, standard_Total_Top_VCs, na.rm=TRUE))
```

``` r
#Create time since graduation variable and dummy variable for missing grad year
Combined_Data_Success_Dummies$`Grad Year of Founder`[is.na(Combined_Data_Success_Dummies$`Grad Year of Founder`)] <- 0

Combined_Data_Success_Dummies$`Grad Year of Founder` <- Combined_Data_Success_Dummies$`Grad Year of Founder` %>% str_remove_all(", .{0,4}") %>% as.numeric()

Combined_Data_Success_Dummies <- Combined_Data_Success_Dummies %>% mutate(missing_grad_year = ifelse(`Grad Year of Founder`== "0", 1,0))

Combined_Data_Success_Dummies <- Combined_Data_Success_Dummies %>% mutate(time_since_grad = ifelse(`Grad Year of Founder` != "0", 2021-`Grad Year of Founder`, 0))
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
write.csv(Combined_Data_Success_Dummies,"C:\\Users\\wdd72\\OneDrive\\Documents\\Junior Fall\\Fintech Practicum\\Fintech_Data\\Combined_Data_For_Regression_11.30.csv", row.names = FALSE)
```

``` r
#summary statistics - School

School_Obs <- Combined_Data_Success_Dummies %>% select(Company, CMC_Dummy, Pomona_Dummy, Scripps_Dummy, Pitzer_Dummy, HMC_Dummy)

  
School_Obs_Narrow <- gather(School_Obs, key="school", value="Dummy", CMC_Dummy, Pomona_Dummy, Scripps_Dummy, Pitzer_Dummy, HMC_Dummy)


School_5C_Summary <- School_Obs_Narrow %>% group_by(school) %>% replace(is.na(.), 0) %>% summarize(Number_of_Founders=sum(Dummy))
School_5C_Summary
```

    ## # A tibble: 5 x 2
    ##   school        Number_of_Founders
    ##   <chr>                      <dbl>
    ## 1 CMC_Dummy                    147
    ## 2 HMC_Dummy                    182
    ## 3 Pitzer_Dummy                  82
    ## 4 Pomona_Dummy                 261
    ## 5 Scripps_Dummy                 21

``` r
#summary statistics - Industry
Industry_Obs <- Combined_Data_Success_Dummies %>% select(Company, Energy_dummy, Materials_dummy, Industrials_dummy, Utilities_dummy, Healthcare_dummy, Financials_dummy, Information_Technology_dummy, Communication_Services_dummy, Real_Estate_dummy, Food_Production_Distribution_dummy, Fine_Arts_dummy, Retail_dummy, Education_dummy, Professional_services_dummy, Entertainment_dummy, Hospitality_Recreation_dummy, Government_dummy, Public_Service_dummy)
Industry_Obs
```

    ## # A tibble: 813 x 19
    ## # Groups:   Company [775]
    ##    Company             Energy_dummy Materials_dummy Industrials_dum~ Utilities_dummy
    ##    <chr>                      <dbl>           <dbl>            <dbl>           <dbl>
    ##  1 BeSababa                       0               0                1               0
    ##  2 54genevels                     0               0                0               0
    ##  3 Traffic Marketplace            0               0                0               0
    ##  4 SMNI                           0               0                0               0
    ##  5 Rebilly                        0               0                0               0
    ##  6 Redocly                        0               0                0               0
    ##  7 PAX Labs                       0               0                0               0
    ##  8 Juul                           0               0                0               0
    ##  9 Comprisma                      0               0                0               0
    ## 10 Cheddr Media                   0               0                0               0
    ## # ... with 803 more rows, and 14 more variables: Healthcare_dummy <dbl>,
    ## #   Financials_dummy <dbl>, Information_Technology_dummy <dbl>,
    ## #   Communication_Services_dummy <dbl>, Real_Estate_dummy <dbl>,
    ## #   Food_Production_Distribution_dummy <dbl>, Fine_Arts_dummy <dbl>,
    ## #   Retail_dummy <dbl>, Education_dummy <dbl>,
    ## #   Professional_services_dummy <dbl>, Entertainment_dummy <dbl>,
    ## #   Hospitality_Recreation_dummy <dbl>, Government_dummy <dbl>, ...

``` r
Industry_Obs_Narrow <- gather(Industry_Obs, key="industry", value="Dummy", Energy_dummy, Materials_dummy, Industrials_dummy, Utilities_dummy, Healthcare_dummy, Financials_dummy, Information_Technology_dummy, Communication_Services_dummy, Real_Estate_dummy, Food_Production_Distribution_dummy, Fine_Arts_dummy, Retail_dummy, Education_dummy, Professional_services_dummy, Entertainment_dummy, Hospitality_Recreation_dummy, Government_dummy, Public_Service_dummy)
Industry_Obs_Narrow
```

    ## # A tibble: 14,634 x 3
    ## # Groups:   Company [775]
    ##    Company             industry     Dummy
    ##    <chr>               <chr>        <dbl>
    ##  1 BeSababa            Energy_dummy     0
    ##  2 54genevels          Energy_dummy     0
    ##  3 Traffic Marketplace Energy_dummy     0
    ##  4 SMNI                Energy_dummy     0
    ##  5 Rebilly             Energy_dummy     0
    ##  6 Redocly             Energy_dummy     0
    ##  7 PAX Labs            Energy_dummy     0
    ##  8 Juul                Energy_dummy     0
    ##  9 Comprisma           Energy_dummy     0
    ## 10 Cheddr Media        Energy_dummy     0
    ## # ... with 14,624 more rows

``` r
Industry_Summary <- Industry_Obs_Narrow %>% group_by(industry) %>% replace(is.na(.), 0) %>% summarize(Number_of_Founders=sum(Dummy)) %>% arrange(desc(Number_of_Founders))
Industry_Summary
```

    ## # A tibble: 18 x 2
    ##    industry                           Number_of_Founders
    ##    <chr>                                           <dbl>
    ##  1 Information_Technology_dummy                      451
    ##  2 Communication_Services_dummy                      395
    ##  3 Education_dummy                                   280
    ##  4 Professional_services_dummy                       268
    ##  5 Financials_dummy                                  245
    ##  6 Healthcare_dummy                                  185
    ##  7 Entertainment_dummy                               121
    ##  8 Public_Service_dummy                               96
    ##  9 Retail_dummy                                       89
    ## 10 Industrials_dummy                                  81
    ## 11 Government_dummy                                   70
    ## 12 Utilities_dummy                                    66
    ## 13 Fine_Arts_dummy                                    47
    ## 14 Food_Production_Distribution_dummy                 37
    ## 15 Hospitality_Recreation_dummy                       23
    ## 16 Real_Estate_dummy                                  23
    ## 17 Materials_dummy                                     9
    ## 18 Energy_dummy                                        3

``` r
#non-standardized success variables distributions

hist_total_capital_raised <- ggplot(data=Combined_Data_Success_Dummies, aes(x=Total_Capital_Raised)) + geom_histogram()
hist_total_capital_raised
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](Dataset-creation-using-Excel_files/figure-gfm/unnamed-chunk-15-1.png)<!-- -->

``` r
hist_Product_Market_Fit <- ggplot(data=Combined_Data_Success_Dummies, aes(x=Product_Market_Fit)) + geom_histogram()
hist_Product_Market_Fit
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](Dataset-creation-using-Excel_files/figure-gfm/unnamed-chunk-15-2.png)<!-- -->

``` r
hist_Total_Financing_Rounds <- ggplot(data=Combined_Data_Success_Dummies, aes(x=Total_Financing_Rounds)) + geom_histogram()
hist_Total_Financing_Rounds
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](Dataset-creation-using-Excel_files/figure-gfm/unnamed-chunk-15-3.png)<!-- -->

``` r
hist_Liquidity_Event_Reached <- ggplot(data=Combined_Data_Success_Dummies, aes(x=Liquidity_Event_Reached)) + geom_histogram()
hist_Liquidity_Event_Reached
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](Dataset-creation-using-Excel_files/figure-gfm/unnamed-chunk-15-4.png)<!-- -->

``` r
hist_length_of_company_life <- ggplot(data=Combined_Data_Success_Dummies, aes(x=length_of_company_life)) + geom_histogram()
hist_length_of_company_life
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

    ## Warning: Removed 29 rows containing non-finite values (stat_bin).

![](Dataset-creation-using-Excel_files/figure-gfm/unnamed-chunk-15-5.png)<!-- -->

``` r
hist_Total_Top_VCs <- ggplot(data=Combined_Data_Success_Dummies, aes(x=Total_Top_VCs)) + geom_histogram()
hist_Total_Top_VCs
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](Dataset-creation-using-Excel_files/figure-gfm/unnamed-chunk-15-6.png)<!-- -->

``` r
#Standardized Success variable distributions

dist_total_capital_raised <- ggplot(data=Combined_Data_Success_Dummies, aes(x=standard_Total_Capital_Raised)) + geom_histogram()
dist_total_capital_raised
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](Dataset-creation-using-Excel_files/figure-gfm/unnamed-chunk-16-1.png)<!-- -->

``` r
dist_Product_Market_Fit <- ggplot(data=Combined_Data_Success_Dummies, aes(x=standard_Product_Market_Fit)) + geom_histogram()
dist_Product_Market_Fit
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](Dataset-creation-using-Excel_files/figure-gfm/unnamed-chunk-16-2.png)<!-- -->

``` r
dist_Total_Financing_Rounds <- ggplot(data=Combined_Data_Success_Dummies, aes(x=standard_Total_Financing_Rounds)) + geom_histogram()
dist_Total_Financing_Rounds
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](Dataset-creation-using-Excel_files/figure-gfm/unnamed-chunk-16-3.png)<!-- -->

``` r
dist_Liquidity_Event_Reached <- ggplot(data=Combined_Data_Success_Dummies, aes(x=standard_Liquidity_Event_Reached)) + geom_histogram()
dist_Liquidity_Event_Reached
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](Dataset-creation-using-Excel_files/figure-gfm/unnamed-chunk-16-4.png)<!-- -->

``` r
dist_length_of_company_life <- ggplot(data=Combined_Data_Success_Dummies, aes(x=standard_length_of_company_life)) + geom_histogram()
dist_length_of_company_life
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

    ## Warning: Removed 29 rows containing non-finite values (stat_bin).

![](Dataset-creation-using-Excel_files/figure-gfm/unnamed-chunk-16-5.png)<!-- -->

``` r
dist_Total_Top_VCs <- ggplot(data=Combined_Data_Success_Dummies, aes(x=standard_Total_Top_VCs)) + geom_histogram()
dist_Total_Top_VCs
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](Dataset-creation-using-Excel_files/figure-gfm/unnamed-chunk-16-6.png)<!-- -->

``` r
dist_Combined_Success_Measure <- ggplot(data=Combined_Data_Success_Dummies, aes(x=Combined_Success_Measure)) + geom_histogram()
dist_Combined_Success_Measure
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](Dataset-creation-using-Excel_files/figure-gfm/unnamed-chunk-16-7.png)<!-- -->

``` r
#Data with outliers removed. Outliers defined as observations with a Combined_Success_Measure greater than 3x the standard deviation of the Combined_Success_Measure.

Data_No_Outliers <- Combined_Data_Success_Dummies %>% group_by(Company) %>% filter(!(Combined_Success_Measure >= sd(Combined_Data_Success_Dummies$Combined_Success_Measure)*3))

write.csv(Data_No_Outliers,"C:\\Users\\wdd72\\OneDrive\\Documents\\Junior Fall\\Fintech Practicum\\Fintech_Data\\Combined_Data_For_Regression_No_Outliers_11.30.csv", row.names = FALSE)
```

``` r
#Standardized Success variable distributions with outliers removed

dist_total_capital_raised_no_out <- ggplot(data=Data_No_Outliers, aes(x=standard_Total_Capital_Raised)) + geom_histogram()
dist_total_capital_raised_no_out
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](Dataset-creation-using-Excel_files/figure-gfm/unnamed-chunk-18-1.png)<!-- -->

``` r
dist_Product_Market_Fit_no_out <- ggplot(data=Data_No_Outliers, aes(x=standard_Product_Market_Fit)) + geom_histogram()
dist_Product_Market_Fit_no_out
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](Dataset-creation-using-Excel_files/figure-gfm/unnamed-chunk-18-2.png)<!-- -->

``` r
dist_Total_Financing_Rounds_no_out <- ggplot(data=Data_No_Outliers, aes(x=standard_Total_Financing_Rounds)) + geom_histogram()
dist_Total_Financing_Rounds_no_out
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](Dataset-creation-using-Excel_files/figure-gfm/unnamed-chunk-18-3.png)<!-- -->

``` r
dist_Liquidity_Event_Reached_no_out <- ggplot(data=Data_No_Outliers, aes(x=standard_Liquidity_Event_Reached)) + geom_histogram()
dist_Liquidity_Event_Reached_no_out
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](Dataset-creation-using-Excel_files/figure-gfm/unnamed-chunk-18-4.png)<!-- -->

``` r
dist_length_of_company_life_no_out <- ggplot(data=Data_No_Outliers, aes(x=standard_length_of_company_life)) + geom_histogram()
dist_length_of_company_life_no_out
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

    ## Warning: Removed 29 rows containing non-finite values (stat_bin).

![](Dataset-creation-using-Excel_files/figure-gfm/unnamed-chunk-18-5.png)<!-- -->

``` r
dist_Total_Top_VCs_no_out <- ggplot(data=Data_No_Outliers, aes(x=standard_Total_Top_VCs)) + geom_histogram()
dist_Total_Top_VCs_no_out
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](Dataset-creation-using-Excel_files/figure-gfm/unnamed-chunk-18-6.png)<!-- -->

``` r
dist_Combined_Success_Measure_no_out <- ggplot(data=Data_No_Outliers, aes(x=Combined_Success_Measure)) + geom_histogram()
dist_Combined_Success_Measure_no_out
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](Dataset-creation-using-Excel_files/figure-gfm/unnamed-chunk-18-7.png)<!-- -->
