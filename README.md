# Fintech-Practicum
Nate Coffin, William DeForest, Ethan Dieck, Samantha Manywa

StoryHouse Ventures Project

Code Explanation and Walk-through: https://claremontmckenna.box.com/s/cawwljzgid4ccyg3gdgmy5ag0oo8tphj

**List of Files**

Data Set Creation Using Excel (.Rmd and .md) - R code used to join the different Excel sheets of data that we had when we originally used Excel to parse the PDL data and create dummy variables.

PDL_Data_Raw1 - PDL data pulled in October. Combined into a single Excel sheet. Education and Experience columns not yet parsed.

Unique_Company_Founder_Obs - Unique company-founder pairs for the list of companies and founders in the "Fintech Practicum View" sheet on Airtable. 

String Parsing.Rmd - R code to search PDL, output the data in .JSON files, convert the .JSON files to .CSV, combine the .CSVs into one sheet, parse the education and experience variables, and finally join the PDL and Airtable data.
