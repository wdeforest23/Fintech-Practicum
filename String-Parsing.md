Automated Data Wrangling
================
William DeForest
11/4/2021

``` r
#import raw PDL data
PDL_Data_raw <- read_excel("C:\\Users\\wdd72\\OneDrive\\Documents\\Junior Fall\\Fintech Practicum\\Fintech_Data\\Superseded\\founder-data1-all data.xlsx")
```

``` r
#separate experience and education strings

Education_Sep <- str_split(PDL_Data_raw$education, "\\}, \\{")
Experience_Sep <- str_split(PDL_Data_raw$experience, "\\}, \\{")
```

``` r
#parse education for school

school <- str_extract_all(Education_Sep,"\\'school': \\{'name': '.{4,100}', 'type'") %>% str_extract_all(": '.+',") %>% str_remove_all(", 'type'\", \"'school': \\{'name':") %>% str_remove("^...") %>% str_remove("..$") %>% str_split("' '", simplify=TRUE) %>% as.data.frame()
```

    ## Warning in stri_extract_all_regex(string, pattern, simplify = simplify, :
    ## argument is not an atomic vector; coercing

    ## Warning in stri_extract_all_regex(string, pattern, simplify = simplify, :
    ## argument is not an atomic vector; coercing

    ## Warning in stri_replace_all_regex(string, pattern,
    ## fix_replacement(replacement), : argument is not an atomic vector; coercing

``` r
school <- school %>% rename("School 1" = V1) %>% rename("School 2" = V2) %>% rename("School 3" = V3) %>% rename("School 4" = V4) %>% rename("School 5" = V5) %>% rename("School 6" = V6) %>% rename("School 7" = V7) %>% rename("School 8" = V8) %>% rename("School 9" = V9)
```

``` r
#parse education for major

major <- str_extract_all(Education_Sep, "'majors': \\[.{0,50}\\], 'minors':") %>% str_remove_all("'majors': ") %>% str_remove_all(", 'minors':") %>% str_extract_all("\\[.*\\]") %>% str_split("\\\", \\\"", simplify=TRUE) %>% as.data.frame()
```

    ## Warning in stri_extract_all_regex(string, pattern, simplify = simplify, :
    ## argument is not an atomic vector; coercing

    ## Warning in stri_replace_all_regex(string, pattern,
    ## fix_replacement(replacement), : argument is not an atomic vector; coercing

    ## Warning in stri_split_regex(string, pattern, n = n, simplify = simplify, :
    ## argument is not an atomic vector; coercing

``` r
major <- major %>% rename("Major 1" = V1) %>% rename("Major 2" = V2) %>% rename("Major 3" = V3) %>% rename("Major 4" = V4) %>% rename("Major 5" = V5) %>% rename("Major 6" = V6) %>% rename("Major 7" = V7) %>% rename("Major 8" = V8) %>% rename("Major 9" = V9) %>% rename("Major 10" = V10)
```

``` r
#parse experience for company

company <- Experience_Sep %>% str_extract_all("'company': \\{'name': .{0,50}, 'size':") %>% str_remove_all("'company': \\{'name': '") %>% str_remove_all("', 'size':") %>% str_remove("^...") %>% str_remove("..$") %>% str_remove_all("\\n") %>% str_split("\\\", \\\"", simplify=TRUE) %>% as.data.frame()
```

    ## Warning in stri_extract_all_regex(string, pattern, simplify = simplify, :
    ## argument is not an atomic vector; coercing

    ## Warning in stri_replace_all_regex(string, pattern,
    ## fix_replacement(replacement), : argument is not an atomic vector; coercing

``` r
company <- company %>% rename("Company 1" = V1) %>% rename("Company 2" = V2) %>% rename("Company 3" = V3) %>% rename("Company 4" = V4) %>% rename("Company 5" = V5) %>% rename("Company 6" = V6) %>% rename("Company 7" = V7) %>% rename("Company 8" = V8) %>% rename("Company 9" = V9) %>% rename("Company 10" = V10) %>% rename("Company 11" = V11) %>% rename("Company 12" = V12) %>% rename("Company 13" = V13) %>% rename("Company 14" = V14) %>% rename("Company 15" = V15) %>% rename("Company 16" = V16) %>% rename("Company 17" = V17) %>% rename("Company 18" = V18) %>% rename("Company 19" = V19) %>% rename("Company 20" = V20) %>% rename("Company 21" = V21) %>% rename("Company 22" = V22) %>% rename("Company 23" = V23) %>% rename("Company 24" = V24) %>% rename("Company 25" = V25) %>% rename("Company 26" = V26) %>% rename("Company 27" = V27) %>% rename("Company 28" = V28) %>% rename("Company 29" = V29) %>% rename("Company 30" = V30) %>% rename("Company 31" = V31) %>% rename("Company 32" = V32) %>% rename("Company 33" = V33) %>% rename("Company 34" = V34) %>% rename("Company 35" = V35) %>% rename("Company 36" = V36) %>% rename("Company 37" = V37) %>% rename("Company 38" = V38) %>% rename("Company 39" = V39) %>% rename("Company 40" = V40) %>% rename("Company 41" = V41) %>% rename("Company 42" = V42) %>% rename("Company 43" = V43) %>% rename("Company 44" = V44) %>% rename("Company 45" = V45) %>% rename("Company 46" = V46)
```

``` r
#merge data frames

PDL_Data <- cbind(PDL_Data_raw, school, major, company)
```

``` r
#output data into Excel
write.csv(PDL_Data,"C:\\Users\\wdd72\\OneDrive\\Documents\\Junior Fall\\Fintech Practicum\\Fintech_Data\\PDL_Data_Parsed.csv", row.names = FALSE)
```

## working space/saved code

%&gt;% str\_remove\_all(“\\"”)

%&gt;% str\_split(“\\\], \\\[”)

%&gt;% str\_split(“,”, simplify=TRUE) %&gt;% as.data.frame()

%&gt;% str\_remove\_all(“\\", \\"”)

%&gt;% str\_extract\_all(“\\\[.{0,50}\\\]”)

%&gt;% str\_remove\_all(“‘majors’:”) %&gt;% str\_remove\_all(“,
‘minors’:”)

%&gt;% str\_extract\_all(“\\\[.\*\\\]”)

school\_dirty &lt;- str\_extract\_all(school\_dirty, “: ‘.{4,100}’,”)
%&gt;% as.character() school\_dirty &lt;-
str\_extract\_all(school\_dirty, “: ‘.{4,100}’,”) school\_dirty2 &lt;-
str\_remove\_all(school\_dirty, “‘school’ : \\{‘name’: ‘“) func &lt;-
function(Education\_Sep) { school\_name &lt;-
str\_extract(Education\_Sep,”\\{’school’: \\{‘name’: ‘.{4,100}’,
‘type’”) major &lt;- str\_extract(Education\_Sep, “‘majors’:
\[‘{4,100}’\], ‘minors’”) data\_frame(school\_name, major) } edulist
&lt;- lapply(Education\_Sep, FUN=func, data=PDL\_Data\_raw)

Education\_Sep &lt;- unlist(Education\_Sep)

    school_name_1 <- str_extract_all(x,"\\{'school': \\{'name': '.{4,100}', 'type'")
    school_name_2 <- str_replace(school_name_dirty, "\\{'school': \\{'name':", " ")
    school_name_3 <- str_extract_all(school_name_2, "'.{4,100}', 'type'")
    school_name_3

    %>% str_c(school_name,sep="-") %>% 
      str_extract_all(": '.{4,100}',") %>% 
      str_remove_all("[,:']") %>% 
      trimws()
    school_name

x\_split &lt;- str\_split(x, “\\{‘school’: \\{‘name’:”) x\_split

a &lt;- “\[{‘company’: {‘name’: ‘the allant group’, ‘size’: ‘51-200’,
‘id’: ‘the-allant-group’, ‘founded’: ‘1984’, ‘industry’: ‘marketing and
advertising’, ‘location’: {‘name’: ‘downers grove, illinois, united
states’, ‘locality’: ‘downers grove’, ‘region’: ’illino”

a

b &lt;- str\_extract(a, “\\\[\\{‘company’: \\{‘name’: ‘\\D+’,”) %&gt;%
str\_extract(“name’:.+”) %&gt;% str\_remove(“name’:”) %&gt;%
str\_remove\_all(“\[’,\]”) %&gt;% trimws()

b

x &lt;- “\[{‘school’: {‘name’: ‘california state university, long
beach’, ‘type’: ‘post-secondary institution’, ‘id’:
‘B7Nor5iR123BEqwt48lJVg\_0’, ‘location’: {‘name’: ‘long beach,
california, united states’, ‘locality’: ‘long beach’, ‘region’:
‘california’, ‘country’: ‘united states’, ‘continent’: ‘north america’},
‘linkedin\_url’:
‘linkedin.com/school/california-state-university-long-beach’,
‘facebook\_url’: ‘facebook.com/csulb’, ‘twitter\_url’:
‘twitter.com/csulb’, ‘linkedin\_id’: ‘17828’, ‘website’: ‘csulb.edu’,
‘domain’: ‘csulb.edu’}, ‘degrees’: \[‘master of science’, ‘masters’\],
‘start\_date’: ‘1976’, ‘end\_date’: None, ‘majors’: \[‘psychology’\],
‘minors’: \[\], ‘gpa’: None}, {‘school’: {‘name’: ‘claremont graduate
university’, ‘type’: ‘post-secondary institution’, ‘id’:
‘5RdUAPiwUnBV1FB0HUuDzA\_0’, ‘location’: {‘name’: ‘claremont,
california, united states’, ‘locality’: ‘claremont’, ‘region’:
‘california’, ‘country’: ‘united states’, ‘continent’: ‘north america’},
‘linkedin\_url’: ‘linkedin.com/school/claremont-graduate-university’,
‘facebook\_url’: ‘facebook.com/claremontgraduateuniversity’,
‘twitter\_url’: ‘twitter.com/cgunews’, ‘linkedin\_id’: ‘17843’,
‘website’: ‘cgu.edu’, ‘domain’: ‘cgu.edu’}, ‘degrees’: \[‘doctorates’,
‘doctor of philosophy’\], ‘start\_date’: ‘1981’, ‘end\_date’: ‘1983’,
‘majors’: \[‘industrial and organizational psychology’\], ‘minors’:
\[\], ‘gpa’: None}, {‘school’: {‘name’: ‘queens college’, ‘type’:
‘post-secondary institution’, ‘id’: ‘7hlkmWGeBtRdgT3SYoiKCQ\_0’,
‘location’: {‘name’: ‘queens, new york, united states’, ‘locality’:
‘queens’, ‘region’: ‘new york’, ‘country’: ‘united states’, ‘continent’:
‘north america’}, ‘linkedin\_url’: ‘linkedin.com/school/queens-college’,
‘facebook\_url’: ‘facebook.com/queenscollege’, ‘twitter\_url’:
‘twitter.com/qc\_news’, ‘linkedin\_id’: ‘18935’, ‘website’:
‘qc.cuny.edu’, ‘domain’: ‘cuny.edu’}, ‘degrees’: \[‘bachelors’,
‘bachelor of arts’\], ‘start\_date’: ‘1971’, ‘end\_date’: ‘1975’,
‘majors’: \[‘economics’, ‘psychology’\], ‘minors’: \[\], ‘gpa’: None},
{‘school’: {‘name’: ‘tel aviv university’, ‘type’: ‘post-secondary
institution’, ‘id’: ‘KGTKnKcOCcRwfhLZS2Rt3g\_0’, ‘location’: {‘name’:
‘tel aviv, israel’, ‘locality’: None, ‘region’: ‘tel aviv’, ‘country’:
‘israel’, ‘continent’: ‘asia’}, ‘linkedin\_url’:
‘linkedin.com/school/tel-aviv-university’, ‘facebook\_url’:
‘facebook.com/tau.main’, ‘twitter\_url’: ‘twitter.com/telavivuni1’,
‘linkedin\_id’: ‘13403’, ‘website’: ‘tau.ac.il’, ‘domain’: ‘tau.ac.il’},
‘degrees’: \[‘masters’, ‘master of arts’\], ‘start\_date’: ‘2020’,
‘end\_date’: None, ‘majors’: \[\], ‘minors’: \[\], ‘gpa’: None},
{‘school’: {‘name’: ‘tel aviv university’, ‘type’: ‘post-secondary
institution’, ‘id’: ‘KGTKnKcOCcRwfhLZS2Rt3g\_0’, ‘location’: {‘name’:
‘tel aviv, israel’, ‘locality’: None, ‘region’: ‘tel aviv’, ‘country’:
‘israel’, ‘continent’: ‘asia’}, ‘linkedin\_url’:
‘linkedin.com/school/tel-aviv-university’, ‘facebook\_url’:
‘facebook.com/tau.main’, ‘twitter\_url’: ‘twitter.com/telavivuni1’,
‘linkedin\_id’: ‘13403’, ‘website’: ‘tau.ac.il’, ‘domain’: ‘tau.ac.il’},
‘end\_date’: ‘2018’, ‘start\_date’: ‘2017’, ‘gpa’: None, ‘degrees’:
\[‘masters’, ‘master of arts’\], ‘majors’: \[‘philosophy’, ‘history’\],
‘minors’: \[\]}\]”

\`\`\`

If a list, should be able to access using \[\[\]\]. Convert to a vector.
as.vector then use apply
