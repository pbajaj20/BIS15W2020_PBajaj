---
title: "Lab 4 Homework"
author: "Priya Bajaj"
date: "2/7/2020"
output:
  html_document:
    keep_md: yes
    theme: spacelab
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove any `#` for included code chunks to run.  

## Load the tidyverse

```r
library(tidyverse)
```

```
## ── Attaching packages ──────────────────────────────────────────────────── tidyverse 1.3.0 ──
```

```
## ✓ ggplot2 3.2.1     ✓ purrr   0.3.3
## ✓ tibble  2.1.3     ✓ dplyr   0.8.3
## ✓ tidyr   1.0.2     ✓ stringr 1.4.0
## ✓ readr   1.3.1     ✓ forcats 0.4.0
```

```
## ── Conflicts ─────────────────────────────────────────────────────── tidyverse_conflicts() ──
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

For this assignment we are going to work with a large dataset from the [United Nations Food and Agriculture Organization](http://www.fao.org/about/en/) on world fisheries. First, load the data.  

1. Load the data `FAO_1950to2012_111914.csv` as a new object titled `fisheries`.

```r
fisheries <- read_csv("data/FAO_1950to2012_111914.csv")
```

```
## Parsed with column specification:
## cols(
##   .default = col_character(),
##   `ISSCAAP group#` = col_double(),
##   `FAO major fishing area` = col_double()
## )
```

```
## See spec(...) for full column specifications.
```

```r
fisheries
```

```
## # A tibble: 17,692 x 71
##    Country `Common name` `ISSCAAP group#` `ISSCAAP taxono… `ASFIS species#`
##    <chr>   <chr>                    <dbl> <chr>            <chr>           
##  1 Albania Angelsharks,…               38 Sharks, rays, c… 10903XXXXX      
##  2 Albania Atlantic bon…               36 Tunas, bonitos,… 1750100101      
##  3 Albania Barracudas n…               37 Miscellaneous p… 17710001XX      
##  4 Albania Blue and red…               45 Shrimps, prawns  2280203101      
##  5 Albania Blue whiting…               32 Cods, hakes, ha… 1480403301      
##  6 Albania Bluefish                    37 Miscellaneous p… 1702021301      
##  7 Albania Bogue                       33 Miscellaneous c… 1703926101      
##  8 Albania Caramote pra…               45 Shrimps, prawns  2280100117      
##  9 Albania Catsharks, n…               38 Sharks, rays, c… 10801003XX      
## 10 Albania Common cuttl…               57 Squids, cuttlef… 3210200202      
## # … with 17,682 more rows, and 66 more variables: `ASFIS species name` <chr>,
## #   `FAO major fishing area` <dbl>, Measure <chr>, `1950` <chr>, `1951` <chr>,
## #   `1952` <chr>, `1953` <chr>, `1954` <chr>, `1955` <chr>, `1956` <chr>,
## #   `1957` <chr>, `1958` <chr>, `1959` <chr>, `1960` <chr>, `1961` <chr>,
## #   `1962` <chr>, `1963` <chr>, `1964` <chr>, `1965` <chr>, `1966` <chr>,
## #   `1967` <chr>, `1968` <chr>, `1969` <chr>, `1970` <chr>, `1971` <chr>,
## #   `1972` <chr>, `1973` <chr>, `1974` <chr>, `1975` <chr>, `1976` <chr>,
## #   `1977` <chr>, `1978` <chr>, `1979` <chr>, `1980` <chr>, `1981` <chr>,
## #   `1982` <chr>, `1983` <chr>, `1984` <chr>, `1985` <chr>, `1986` <chr>,
## #   `1987` <chr>, `1988` <chr>, `1989` <chr>, `1990` <chr>, `1991` <chr>,
## #   `1992` <chr>, `1993` <chr>, `1994` <chr>, `1995` <chr>, `1996` <chr>,
## #   `1997` <chr>, `1998` <chr>, `1999` <chr>, `2000` <chr>, `2001` <chr>,
## #   `2002` <chr>, `2003` <chr>, `2004` <chr>, `2005` <chr>, `2006` <chr>,
## #   `2007` <chr>, `2008` <chr>, `2009` <chr>, `2010` <chr>, `2011` <chr>,
## #   `2012` <chr>
```
2. What are the names of the columns? Do you see any potential problems with the column names?

```r
colnames(fisheries)
```

```
##  [1] "Country"                 "Common name"            
##  [3] "ISSCAAP group#"          "ISSCAAP taxonomic group"
##  [5] "ASFIS species#"          "ASFIS species name"     
##  [7] "FAO major fishing area"  "Measure"                
##  [9] "1950"                    "1951"                   
## [11] "1952"                    "1953"                   
## [13] "1954"                    "1955"                   
## [15] "1956"                    "1957"                   
## [17] "1958"                    "1959"                   
## [19] "1960"                    "1961"                   
## [21] "1962"                    "1963"                   
## [23] "1964"                    "1965"                   
## [25] "1966"                    "1967"                   
## [27] "1968"                    "1969"                   
## [29] "1970"                    "1971"                   
## [31] "1972"                    "1973"                   
## [33] "1974"                    "1975"                   
## [35] "1976"                    "1977"                   
## [37] "1978"                    "1979"                   
## [39] "1980"                    "1981"                   
## [41] "1982"                    "1983"                   
## [43] "1984"                    "1985"                   
## [45] "1986"                    "1987"                   
## [47] "1988"                    "1989"                   
## [49] "1990"                    "1991"                   
## [51] "1992"                    "1993"                   
## [53] "1994"                    "1995"                   
## [55] "1996"                    "1997"                   
## [57] "1998"                    "1999"                   
## [59] "2000"                    "2001"                   
## [61] "2002"                    "2003"                   
## [63] "2004"                    "2005"                   
## [65] "2006"                    "2007"                   
## [67] "2008"                    "2009"                   
## [69] "2010"                    "2011"                   
## [71] "2012"
```

3. What is the structure of the data? Show the classes of each variable.

```r
sapply(fisheries, class)
```

```
##                 Country             Common name          ISSCAAP group# 
##             "character"             "character"               "numeric" 
## ISSCAAP taxonomic group          ASFIS species#      ASFIS species name 
##             "character"             "character"             "character" 
##  FAO major fishing area                 Measure                    1950 
##               "numeric"             "character"             "character" 
##                    1951                    1952                    1953 
##             "character"             "character"             "character" 
##                    1954                    1955                    1956 
##             "character"             "character"             "character" 
##                    1957                    1958                    1959 
##             "character"             "character"             "character" 
##                    1960                    1961                    1962 
##             "character"             "character"             "character" 
##                    1963                    1964                    1965 
##             "character"             "character"             "character" 
##                    1966                    1967                    1968 
##             "character"             "character"             "character" 
##                    1969                    1970                    1971 
##             "character"             "character"             "character" 
##                    1972                    1973                    1974 
##             "character"             "character"             "character" 
##                    1975                    1976                    1977 
##             "character"             "character"             "character" 
##                    1978                    1979                    1980 
##             "character"             "character"             "character" 
##                    1981                    1982                    1983 
##             "character"             "character"             "character" 
##                    1984                    1985                    1986 
##             "character"             "character"             "character" 
##                    1987                    1988                    1989 
##             "character"             "character"             "character" 
##                    1990                    1991                    1992 
##             "character"             "character"             "character" 
##                    1993                    1994                    1995 
##             "character"             "character"             "character" 
##                    1996                    1997                    1998 
##             "character"             "character"             "character" 
##                    1999                    2000                    2001 
##             "character"             "character"             "character" 
##                    2002                    2003                    2004 
##             "character"             "character"             "character" 
##                    2005                    2006                    2007 
##             "character"             "character"             "character" 
##                    2008                    2009                    2010 
##             "character"             "character"             "character" 
##                    2011                    2012 
##             "character"             "character"
```


4. Think about the classes. Will any present problems? Make any changes you think are necessary below.
##Year should be a numeric not a character. Everything else should be a factor

```r
fisheries <- fisheries %>% 
  mutate_at(vars(starts_with("19")), as.numeric) %>% 
  mutate_at(vars(starts_with("2")), as.numeric) %>% 
  mutate_if(is.character, as.factor)
```

```
## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion

## Warning: NAs introduced by coercion
```


```r
sapply(fisheries, class)
```

```
##                 Country             Common name          ISSCAAP group# 
##                "factor"                "factor"               "numeric" 
## ISSCAAP taxonomic group          ASFIS species#      ASFIS species name 
##                "factor"                "factor"                "factor" 
##  FAO major fishing area                 Measure                    1950 
##               "numeric"                "factor"               "numeric" 
##                    1951                    1952                    1953 
##               "numeric"               "numeric"               "numeric" 
##                    1954                    1955                    1956 
##               "numeric"               "numeric"               "numeric" 
##                    1957                    1958                    1959 
##               "numeric"               "numeric"               "numeric" 
##                    1960                    1961                    1962 
##               "numeric"               "numeric"               "numeric" 
##                    1963                    1964                    1965 
##               "numeric"               "numeric"               "numeric" 
##                    1966                    1967                    1968 
##               "numeric"               "numeric"               "numeric" 
##                    1969                    1970                    1971 
##               "numeric"               "numeric"               "numeric" 
##                    1972                    1973                    1974 
##               "numeric"               "numeric"               "numeric" 
##                    1975                    1976                    1977 
##               "numeric"               "numeric"               "numeric" 
##                    1978                    1979                    1980 
##               "numeric"               "numeric"               "numeric" 
##                    1981                    1982                    1983 
##               "numeric"               "numeric"               "numeric" 
##                    1984                    1985                    1986 
##               "numeric"               "numeric"               "numeric" 
##                    1987                    1988                    1989 
##               "numeric"               "numeric"               "numeric" 
##                    1990                    1991                    1992 
##               "numeric"               "numeric"               "numeric" 
##                    1993                    1994                    1995 
##               "numeric"               "numeric"               "numeric" 
##                    1996                    1997                    1998 
##               "numeric"               "numeric"               "numeric" 
##                    1999                    2000                    2001 
##               "numeric"               "numeric"               "numeric" 
##                    2002                    2003                    2004 
##               "numeric"               "numeric"               "numeric" 
##                    2005                    2006                    2007 
##               "numeric"               "numeric"               "numeric" 
##                    2008                    2009                    2010 
##               "numeric"               "numeric"               "numeric" 
##                    2011                    2012 
##               "numeric"               "numeric"
```
5. How many countries are represented in the data? Provide a count.

```r
nlevels(fisheries$Country)
```

```
## [1] 204
```

6. What are the names of the countries?

```r
levels(fisheries$Country)
```

```
##   [1] "Albania"                   "Algeria"                  
##   [3] "American Samoa"            "Angola"                   
##   [5] "Anguilla"                  "Antigua and Barbuda"      
##   [7] "Argentina"                 "Aruba"                    
##   [9] "Australia"                 "Bahamas"                  
##  [11] "Bahrain"                   "Bangladesh"               
##  [13] "Barbados"                  "Belgium"                  
##  [15] "Belize"                    "Benin"                    
##  [17] "Bermuda"                   "Bonaire/S.Eustatius/Saba" 
##  [19] "Bosnia and Herzegovina"    "Brazil"                   
##  [21] "British Indian Ocean Ter"  "British Virgin Islands"   
##  [23] "Brunei Darussalam"         "Bulgaria"                 
##  [25] "Cabo Verde"                "Cambodia"                 
##  [27] "Cameroon"                  "Canada"                   
##  [29] "Cayman Islands"            "Channel Islands"          
##  [31] "Chile"                     "China"                    
##  [33] "China, Hong Kong SAR"      "China, Macao SAR"         
##  [35] "Colombia"                  "Comoros"                  
##  [37] "Congo, Dem. Rep. of the"   "Congo, Republic of"       
##  [39] "Cook Islands"              "Costa Rica"               
##  [41] "Croatia"                   "Cuba"                     
##  [43] "Cura\xe7ao"                "Cyprus"                   
##  [45] "C\xf4te d'Ivoire"          "Denmark"                  
##  [47] "Djibouti"                  "Dominica"                 
##  [49] "Dominican Republic"        "Ecuador"                  
##  [51] "Egypt"                     "El Salvador"              
##  [53] "Equatorial Guinea"         "Eritrea"                  
##  [55] "Estonia"                   "Ethiopia"                 
##  [57] "Falkland Is.(Malvinas)"    "Faroe Islands"            
##  [59] "Fiji, Republic of"         "Finland"                  
##  [61] "France"                    "French Guiana"            
##  [63] "French Polynesia"          "French Southern Terr"     
##  [65] "Gabon"                     "Gambia"                   
##  [67] "Georgia"                   "Germany"                  
##  [69] "Ghana"                     "Gibraltar"                
##  [71] "Greece"                    "Greenland"                
##  [73] "Grenada"                   "Guadeloupe"               
##  [75] "Guam"                      "Guatemala"                
##  [77] "Guinea"                    "GuineaBissau"             
##  [79] "Guyana"                    "Haiti"                    
##  [81] "Honduras"                  "Iceland"                  
##  [83] "India"                     "Indonesia"                
##  [85] "Iran (Islamic Rep. of)"    "Iraq"                     
##  [87] "Ireland"                   "Isle of Man"              
##  [89] "Israel"                    "Italy"                    
##  [91] "Jamaica"                   "Japan"                    
##  [93] "Jordan"                    "Kenya"                    
##  [95] "Kiribati"                  "Korea, Dem. People's Rep" 
##  [97] "Korea, Republic of"        "Kuwait"                   
##  [99] "Latvia"                    "Lebanon"                  
## [101] "Liberia"                   "Libya"                    
## [103] "Lithuania"                 "Madagascar"               
## [105] "Malaysia"                  "Maldives"                 
## [107] "Malta"                     "Marshall Islands"         
## [109] "Martinique"                "Mauritania"               
## [111] "Mauritius"                 "Mayotte"                  
## [113] "Mexico"                    "Micronesia, Fed.States of"
## [115] "Monaco"                    "Montenegro"               
## [117] "Montserrat"                "Morocco"                  
## [119] "Mozambique"                "Myanmar"                  
## [121] "Namibia"                   "Nauru"                    
## [123] "Netherlands"               "Netherlands Antilles"     
## [125] "New Caledonia"             "New Zealand"              
## [127] "Nicaragua"                 "Nigeria"                  
## [129] "Niue"                      "Norfolk Island"           
## [131] "Northern Mariana Is."      "Norway"                   
## [133] "Oman"                      "Other nei"                
## [135] "Pakistan"                  "Palau"                    
## [137] "Palestine, Occupied Tr."   "Panama"                   
## [139] "Papua New Guinea"          "Peru"                     
## [141] "Philippines"               "Pitcairn Islands"         
## [143] "Poland"                    "Portugal"                 
## [145] "Puerto Rico"               "Qatar"                    
## [147] "Romania"                   "Russian Federation"       
## [149] "R\xe9union"                "Saint Barth\xe9lemy"      
## [151] "Saint Helena"              "Saint Kitts and Nevis"    
## [153] "Saint Lucia"               "Saint Vincent/Grenadines" 
## [155] "SaintMartin"               "Samoa"                    
## [157] "Sao Tome and Principe"     "Saudi Arabia"             
## [159] "Senegal"                   "Serbia and Montenegro"    
## [161] "Seychelles"                "Sierra Leone"             
## [163] "Singapore"                 "Sint Maarten"             
## [165] "Slovenia"                  "Solomon Islands"          
## [167] "Somalia"                   "South Africa"             
## [169] "Spain"                     "Sri Lanka"                
## [171] "St. Pierre and Miquelon"   "Sudan"                    
## [173] "Sudan (former)"            "Suriname"                 
## [175] "Svalbard and Jan Mayen"    "Sweden"                   
## [177] "Syrian Arab Republic"      "Taiwan Province of China" 
## [179] "Tanzania, United Rep. of"  "Thailand"                 
## [181] "TimorLeste"                "Togo"                     
## [183] "Tokelau"                   "Tonga"                    
## [185] "Trinidad and Tobago"       "Tunisia"                  
## [187] "Turkey"                    "Turks and Caicos Is."     
## [189] "Tuvalu"                    "Ukraine"                  
## [191] "Un. Sov. Soc. Rep."        "United Arab Emirates"     
## [193] "United Kingdom"            "United States of America" 
## [195] "Uruguay"                   "US Virgin Islands"        
## [197] "Vanuatu"                   "Venezuela, Boliv Rep of"  
## [199] "Viet Nam"                  "Wallis and Futuna Is."    
## [201] "Western Sahara"            "Yemen"                    
## [203] "Yugoslavia SFR"            "Zanzibar"
```

7. Use `rename()` to rename the columns and make them easier to use. The new column names should be:  
+ country
+ commname
+ ASFIS_sciname
+ ASFIS_spcode
+ ISSCAAP_spgroup
+ ISSCAAP_spgroupname
+ FAO_area
+ unit


```r
fisheries2 <- fisheries %>% 
  rename(country="Country", commname="Common name", ISSCAAP_spgroup="ISSCAAP group#",  "ISSCAAP_spgroupname"="ISSCAAP taxonomic group" , "ASFIS_spcode"="ASFIS species#", ASFIS_sciname="ASFIS species name", FAO_area="FAO major fishing area", unit="Measure")
```

8. Are these data tidy? Why or why not, and, how do you know? Use the appropriate pivot function to tidy the data. Remove the NA's. Put the tidy data frame into a new object `fisheries_tidy`.  

```r
fisheries_tidy <- fisheries2 %>% 
  pivot_longer(-c(country, commname, ASFIS_spcode, ASFIS_sciname, ISSCAAP_spgroupname, ISSCAAP_spgroup, FAO_area, unit), 
               names_to = "year",
               values_to = "catch")
fisheries_tidy
```

```
## # A tibble: 1,114,596 x 10
##    country commname ISSCAAP_spgroup ISSCAAP_spgroup… ASFIS_spcode ASFIS_sciname
##    <fct>   <fct>              <dbl> <fct>            <fct>        <fct>        
##  1 Albania Angelsh…              38 Sharks, rays, c… 10903XXXXX   Squatinidae  
##  2 Albania Angelsh…              38 Sharks, rays, c… 10903XXXXX   Squatinidae  
##  3 Albania Angelsh…              38 Sharks, rays, c… 10903XXXXX   Squatinidae  
##  4 Albania Angelsh…              38 Sharks, rays, c… 10903XXXXX   Squatinidae  
##  5 Albania Angelsh…              38 Sharks, rays, c… 10903XXXXX   Squatinidae  
##  6 Albania Angelsh…              38 Sharks, rays, c… 10903XXXXX   Squatinidae  
##  7 Albania Angelsh…              38 Sharks, rays, c… 10903XXXXX   Squatinidae  
##  8 Albania Angelsh…              38 Sharks, rays, c… 10903XXXXX   Squatinidae  
##  9 Albania Angelsh…              38 Sharks, rays, c… 10903XXXXX   Squatinidae  
## 10 Albania Angelsh…              38 Sharks, rays, c… 10903XXXXX   Squatinidae  
## # … with 1,114,586 more rows, and 4 more variables: FAO_area <dbl>, unit <fct>,
## #   year <chr>, catch <dbl>
```
9. Refocus the data only to include country, ISSCAAP_spgroupname, ASFIS_spcode, ASFIS_sciname, year, and catch.

```r
fisheries_tidy2 <- fisheries_tidy %>% 
  select(country, ISSCAAP_spgroupname, ASFIS_spcode, ASFIS_sciname, year, catch)
fisheries_tidy2
```

```
## # A tibble: 1,114,596 x 6
##    country ISSCAAP_spgroupname     ASFIS_spcode ASFIS_sciname year  catch
##    <fct>   <fct>                   <fct>        <fct>         <chr> <dbl>
##  1 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   1950     NA
##  2 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   1951     NA
##  3 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   1952     NA
##  4 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   1953     NA
##  5 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   1954     NA
##  6 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   1955     NA
##  7 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   1956     NA
##  8 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   1957     NA
##  9 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   1958     NA
## 10 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   1959     NA
## # … with 1,114,586 more rows
```

10. Re-check the classes of `fisheries_tidy2`. Notice that "catch" is shown as a character! This is a problem because we will want to treat it as a numeric. How will you deal with this?

```r
sapply(fisheries_tidy2,class)
```

```
##             country ISSCAAP_spgroupname        ASFIS_spcode       ASFIS_sciname 
##            "factor"            "factor"            "factor"            "factor" 
##                year               catch 
##         "character"           "numeric"
```


```r
fisheries_tidy2$catch <- as.numeric(fisheries_tidy2$catch)
```

11. Based on the ASFIS_spcode, how many distinct taxa were caught as part of these data?

```r
nlevels(fisheries_tidy2$ASFIS_spcode)
```

```
## [1] 1553
```

12. Which country had the largest overall catch in the year 2000?

```r
fisheries_tidy2 %>%
 filter(year=="2000")  %>% 
group_by(country) %>% 
  summarize(catch = sum(catch,na.rm=T)) %>% 
  arrange(desc(catch))
```

```
## # A tibble: 204 x 2
##    country                     catch
##    <fct>                       <dbl>
##  1 Peru                     10625010
##  2 Japan                     4921013
##  3 United States of America  4692229
##  4 Chile                     4297928
##  5 Indonesia                 3761769
##  6 Russian Federation        3678828
##  7 Thailand                  2795719
##  8 India                     2760632
##  9 Norway                    2698506
## 10 Iceland                   1982369
## # … with 194 more rows
```
##Peru

13. Which country caught the most sardines (_Sardina_) between the years 1990-2000?

```r
fisheries_tidy2 %>%
  group_by(country) %>% 
  filter(year >=1990 & year<=2000) %>% 
  filter(ASFIS_sciname == "Sardina pilchardus") %>%
  summarize(catch = sum(catch, na.rm=T)) %>% 
  arrange(desc(catch))
```

```
## # A tibble: 46 x 2
##    country              catch
##    <fct>                <dbl>
##  1 Morocco            4785190
##  2 Spain              1425317
##  3 Russian Federation 1035139
##  4 Portugal            926318
##  5 Ukraine             784730
##  6 Italy               377907
##  7 Algeria             311733
##  8 Turkey              273565
##  9 France              263871
## 10 Denmark             242017
## # … with 36 more rows
```

14. Which five countries caught the most cephalopods between 2008-2012?

```r
fisheries_tidy2 %>% 
  filter(str_detect(ISSCAAP_spgroupname, "Squids")) %>% 
  filter(year <= 2012 & year >= 2008) %>% 
  group_by(country) %>% 
  summarize(catch = sum(catch, na.rm = T)) %>% 
  arrange(desc(catch, by.group = TRUE))
```

```
## # A tibble: 139 x 2
##    country                    catch
##    <fct>                      <dbl>
##  1 China                    4785139
##  2 Peru                     2274232
##  3 Korea, Republic of       1535454
##  4 Japan                    1394041
##  5 Chile                     723186
##  6 Indonesia                 684567
##  7 United States of America  613400
##  8 Thailand                  603529
##  9 Taiwan Province of China  593638
## 10 Argentina                 587238
## # … with 129 more rows
```

15. Given the top five countries from question 12 above, which species was the highest catch total? The lowest?

```r
fisheries_tidy2 %>% 
  filter(str_detect(ISSCAAP_spgroupname, "Squids")) %>% 
  filter(year <= 2012 & year >= 2008) %>% 
  group_by(ASFIS_sciname) %>% 
  summarize(catch_total=sum(catch, na.rm=T)) %>% 
  arrange(desc(catch_total))
```

```
## # A tibble: 35 x 2
##    ASFIS_sciname               catch_total
##    <fct>                             <dbl>
##  1 Dosidicus gigas                 4211138
##  2 Loliginidae, Ommastrephidae     2822078
##  3 Illex argentinus                1834620
##  4 Todarodes pacificus             1767506
##  5 Octopodidae                     1458746
##  6 Sepiidae, Sepiolidae            1331357
##  7 Loligo spp                      1291035
##  8 Cephalopoda                      735839
##  9 Loligo opalescens                477536
## 10 Loligo gahi                      317535
## # … with 25 more rows
```


```r
fisheries_tidy2 %>% 
  filter(str_detect(ISSCAAP_spgroupname, "Squids")) %>% 
  filter(year <= 2012 & year >= 2008) %>% 
  group_by(ASFIS_sciname) %>% 
  summarize(catch_total=sum(catch, na.rm=T)) %>% 
  arrange(catch_total)
```

```
## # A tibble: 35 x 2
##    ASFIS_sciname        catch_total
##    <fct>                      <dbl>
##  1 Eledone moschata               0
##  2 Gonatidae                      0
##  3 Moroteuthis robustus           0
##  4 Pareledone spp                 0
##  5 Todarodes filippovae           1
##  6 Martialia hyadesi              4
##  7 Moroteuthis ingens           194
##  8 Loligo vulgaris              398
##  9 Eledone cirrhosa             920
## 10 Loligo duvauceli            1843
## # … with 25 more rows
```

16. In some cases, the taxonomy of the fish being caught is unclear. Make a new data frame called `coastal_fish` that shows the taxonomic composition of "Miscellaneous coastal fishes" within the ISSCAAP_spgroupname column.

```r
coastal_fish <- fisheries_tidy2 %>% 
  filter(ISSCAAP_spgroupname == 'Miscellaneous coastal fishes')
```

17. Use the data to do at least one exploratory analysis of your choice. What can you learn?
##I want to see which country had the highest overall catch numbers

```r
fisheries_tidy2 %>%
  group_by(country) %>% 
  summarize(catch = sum(catch, na.rm=T)) %>% 
  arrange(desc(catch))
```

```
## # A tibble: 204 x 2
##    country                      catch
##    <fct>                        <dbl>
##  1 Japan                    422374927
##  2 Peru                     353245326
##  3 China                    245615855
##  4 United States of America 234185488
##  5 Un. Sov. Soc. Rep.       208146847
##  6 Chile                    176996266
##  7 Norway                   143337763
##  8 Indonesia                126866466
##  9 India                    109839496
## 10 Russian Federation       105965392
## # … with 194 more rows
```
## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
