---
title: "BIS 15L Practice Midterm"
output:
  html_document:
    keep_md: yes
    theme: spacelab
---



## `gapminder`
For this assignment, we are going to use the dataset [gapminder](https://cran.r-project.org/web/packages/gapminder/index.html). Gapminder includes information about economics, population, and life expectancy from countries all over the world. You will need to install it before use.

```r
#install.packages("gapminder")
```

## Load the libraries

```r
library(tidyverse)
```

```
## ── Attaching packages ──────────────────────────────────────────────────────────────────────── tidyverse 1.3.0 ──
```

```
## ✓ ggplot2 3.2.1     ✓ purrr   0.3.3
## ✓ tibble  2.1.3     ✓ dplyr   0.8.4
## ✓ tidyr   1.0.2     ✓ stringr 1.4.0
## ✓ readr   1.3.1     ✓ forcats 0.4.0
```

```
## ── Conflicts ─────────────────────────────────────────────────────────────────────────── tidyverse_conflicts() ──
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

```r
library(gapminder)
options(scipen=999) #disables scientific notation when printing
```

## Data structure
**1. Use the function(s) of your choice to get an idea of the overall structure of the data frame, including its dimensions, column names, variable classes, etc.**

```r
dim(gapminder)
```

```
## [1] 1704    6
```


```r
colnames(gapminder)
```

```
## [1] "country"   "continent" "year"      "lifeExp"   "pop"       "gdpPercap"
```


```r
str(gapminder)
```

```
## Classes 'tbl_df', 'tbl' and 'data.frame':	1704 obs. of  6 variables:
##  $ country  : Factor w/ 142 levels "Afghanistan",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ continent: Factor w/ 5 levels "Africa","Americas",..: 3 3 3 3 3 3 3 3 3 3 ...
##  $ year     : int  1952 1957 1962 1967 1972 1977 1982 1987 1992 1997 ...
##  $ lifeExp  : num  28.8 30.3 32 34 36.1 ...
##  $ pop      : int  8425333 9240934 10267083 11537966 13079460 14880372 12881816 13867957 16317921 22227415 ...
##  $ gdpPercap: num  779 821 853 836 740 ...
```



**2. Are there any NA's in the data?**

```r
anyNA(gapminder)
```

```
## [1] FALSE
```

## Three versions of the `gampminder` data  
We will use three versions of the `gapminder` data to perform analyses and (eventually) make plots. For now, make the following long and wide versions of `gapminder`.

## `gapminder`
Notice that `gapminder` has one row for each country and year, and one column for each measurement (lifeExp, pop, gdpPercap).

```r
gapminder <- gapminder
gapminder
```

```
## # A tibble: 1,704 x 6
##    country     continent  year lifeExp      pop gdpPercap
##    <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
##  1 Afghanistan Asia       1952    28.8  8425333      779.
##  2 Afghanistan Asia       1957    30.3  9240934      821.
##  3 Afghanistan Asia       1962    32.0 10267083      853.
##  4 Afghanistan Asia       1967    34.0 11537966      836.
##  5 Afghanistan Asia       1972    36.1 13079460      740.
##  6 Afghanistan Asia       1977    38.4 14880372      786.
##  7 Afghanistan Asia       1982    39.9 12881816      978.
##  8 Afghanistan Asia       1987    40.8 13867957      852.
##  9 Afghanistan Asia       1992    41.7 16317921      649.
## 10 Afghanistan Asia       1997    41.8 22227415      635.
## # … with 1,694 more rows
```

## Long `gapminder`
**3. Make a new data frame `gapminder_long` that combines the three measured values (lifeExp, pop, gdpPercap) into a single column associated with a country and year.**

```r
gapminder_long <- 
  gapminder %>% 
  pivot_longer(lifeExp:gdpPercap,
               names_to = "observation",
               values_to = "measurement") %>% 
  unite("country_year",country,year)
  
  

  
gapminder_long
```

```
## # A tibble: 5,112 x 4
##    country_year     continent observation measurement
##    <chr>            <fct>     <chr>             <dbl>
##  1 Afghanistan_1952 Asia      lifeExp            28.8
##  2 Afghanistan_1952 Asia      pop           8425333  
##  3 Afghanistan_1952 Asia      gdpPercap         779. 
##  4 Afghanistan_1957 Asia      lifeExp            30.3
##  5 Afghanistan_1957 Asia      pop           9240934  
##  6 Afghanistan_1957 Asia      gdpPercap         821. 
##  7 Afghanistan_1962 Asia      lifeExp            32.0
##  8 Afghanistan_1962 Asia      pop          10267083  
##  9 Afghanistan_1962 Asia      gdpPercap         853. 
## 10 Afghanistan_1967 Asia      lifeExp            34.0
## # … with 5,102 more rows
```


**4. For practice, use `pivot_wider()` to put the data back into the original `gapminder` format.**

```r
gapminder_long %>% 
  separate(country_year, into = c("country","year"), sep = "_") %>% 
  pivot_wider(names_from = "observation",
              values_from = "measurement") 
```

```
## # A tibble: 1,704 x 6
##    country     year  continent lifeExp      pop gdpPercap
##    <chr>       <chr> <fct>       <dbl>    <dbl>     <dbl>
##  1 Afghanistan 1952  Asia         28.8  8425333      779.
##  2 Afghanistan 1957  Asia         30.3  9240934      821.
##  3 Afghanistan 1962  Asia         32.0 10267083      853.
##  4 Afghanistan 1967  Asia         34.0 11537966      836.
##  5 Afghanistan 1972  Asia         36.1 13079460      740.
##  6 Afghanistan 1977  Asia         38.4 14880372      786.
##  7 Afghanistan 1982  Asia         39.9 12881816      978.
##  8 Afghanistan 1987  Asia         40.8 13867957      852.
##  9 Afghanistan 1992  Asia         41.7 16317921      649.
## 10 Afghanistan 1997  Asia         41.8 22227415      635.
## # … with 1,694 more rows
```


## Wide `gapminder`
**5. Make a new data frame `gapminder_wide` that has all observations for each country in a single row. The column names should be named as "observation_year". Arrange them sequentially by year.**

```r
gapminder_wide <- 
  gapminder_long %>%
  separate(country_year, into = c("country", "year"), sep = "_") %>% 
  unite("observation_year", observation, year) %>% 
  pivot_wider(names_from = "observation_year",
              values_from = "measurement")
  
gapminder_wide 
```

```
## # A tibble: 142 x 38
##    country continent lifeExp_1952 pop_1952 gdpPercap_1952 lifeExp_1957 pop_1957
##    <chr>   <fct>            <dbl>    <dbl>          <dbl>        <dbl>    <dbl>
##  1 Afghan… Asia              28.8  8425333           779.         30.3  9240934
##  2 Albania Europe            55.2  1282697          1601.         59.3  1476505
##  3 Algeria Africa            43.1  9279525          2449.         45.7 10270856
##  4 Angola  Africa            30.0  4232095          3521.         32.0  4561361
##  5 Argent… Americas          62.5 17876956          5911.         64.4 19610538
##  6 Austra… Oceania           69.1  8691212         10040.         70.3  9712569
##  7 Austria Europe            66.8  6927772          6137.         67.5  6965860
##  8 Bahrain Asia              50.9   120447          9867.         53.8   138655
##  9 Bangla… Asia              37.5 46886859           684.         39.3 51365468
## 10 Belgium Europe            68    8730405          8343.         69.2  8989111
## # … with 132 more rows, and 31 more variables: gdpPercap_1957 <dbl>,
## #   lifeExp_1962 <dbl>, pop_1962 <dbl>, gdpPercap_1962 <dbl>,
## #   lifeExp_1967 <dbl>, pop_1967 <dbl>, gdpPercap_1967 <dbl>,
## #   lifeExp_1972 <dbl>, pop_1972 <dbl>, gdpPercap_1972 <dbl>,
## #   lifeExp_1977 <dbl>, pop_1977 <dbl>, gdpPercap_1977 <dbl>,
## #   lifeExp_1982 <dbl>, pop_1982 <dbl>, gdpPercap_1982 <dbl>,
## #   lifeExp_1987 <dbl>, pop_1987 <dbl>, gdpPercap_1987 <dbl>,
## #   lifeExp_1992 <dbl>, pop_1992 <dbl>, gdpPercap_1992 <dbl>,
## #   lifeExp_1997 <dbl>, pop_1997 <dbl>, gdpPercap_1997 <dbl>,
## #   lifeExp_2002 <dbl>, pop_2002 <dbl>, gdpPercap_2002 <dbl>,
## #   lifeExp_2007 <dbl>, pop_2007 <dbl>, gdpPercap_2007 <dbl>
```


**6. For practice, use `pivot_longer()` to put the data back into the original `gapminder` format. Hint: you can't do this in one step!**

```r
gapminder_wide %>% 
  pivot_longer(-c(country, continent),
               names_to = "observation_year",
               values_to = "measurements") %>% 
  separate(observation_year, into = c("observation", "year"), sep = "_") %>% 
  pivot_wider(names_from = "observation",
              values_from = "measurements")
```

```
## # A tibble: 1,704 x 6
##    country     continent year  lifeExp      pop gdpPercap
##    <chr>       <fct>     <chr>   <dbl>    <dbl>     <dbl>
##  1 Afghanistan Asia      1952     28.8  8425333      779.
##  2 Afghanistan Asia      1957     30.3  9240934      821.
##  3 Afghanistan Asia      1962     32.0 10267083      853.
##  4 Afghanistan Asia      1967     34.0 11537966      836.
##  5 Afghanistan Asia      1972     36.1 13079460      740.
##  6 Afghanistan Asia      1977     38.4 14880372      786.
##  7 Afghanistan Asia      1982     39.9 12881816      978.
##  8 Afghanistan Asia      1987     40.8 13867957      852.
##  9 Afghanistan Asia      1992     41.7 16317921      649.
## 10 Afghanistan Asia      1997     41.8 22227415      635.
## # … with 1,694 more rows
```


## Data summaries
**7. How many different continents and countries are represented in the data? Provide the total number and their names.**

```r
summarize(gapminder, countries = n_distinct(country))
```

```
## # A tibble: 1 x 1
##   countries
##       <int>
## 1       142
```

```r
unique(gapminder$country)
```

```
##   [1] Afghanistan              Albania                  Algeria                 
##   [4] Angola                   Argentina                Australia               
##   [7] Austria                  Bahrain                  Bangladesh              
##  [10] Belgium                  Benin                    Bolivia                 
##  [13] Bosnia and Herzegovina   Botswana                 Brazil                  
##  [16] Bulgaria                 Burkina Faso             Burundi                 
##  [19] Cambodia                 Cameroon                 Canada                  
##  [22] Central African Republic Chad                     Chile                   
##  [25] China                    Colombia                 Comoros                 
##  [28] Congo, Dem. Rep.         Congo, Rep.              Costa Rica              
##  [31] Cote d'Ivoire            Croatia                  Cuba                    
##  [34] Czech Republic           Denmark                  Djibouti                
##  [37] Dominican Republic       Ecuador                  Egypt                   
##  [40] El Salvador              Equatorial Guinea        Eritrea                 
##  [43] Ethiopia                 Finland                  France                  
##  [46] Gabon                    Gambia                   Germany                 
##  [49] Ghana                    Greece                   Guatemala               
##  [52] Guinea                   Guinea-Bissau            Haiti                   
##  [55] Honduras                 Hong Kong, China         Hungary                 
##  [58] Iceland                  India                    Indonesia               
##  [61] Iran                     Iraq                     Ireland                 
##  [64] Israel                   Italy                    Jamaica                 
##  [67] Japan                    Jordan                   Kenya                   
##  [70] Korea, Dem. Rep.         Korea, Rep.              Kuwait                  
##  [73] Lebanon                  Lesotho                  Liberia                 
##  [76] Libya                    Madagascar               Malawi                  
##  [79] Malaysia                 Mali                     Mauritania              
##  [82] Mauritius                Mexico                   Mongolia                
##  [85] Montenegro               Morocco                  Mozambique              
##  [88] Myanmar                  Namibia                  Nepal                   
##  [91] Netherlands              New Zealand              Nicaragua               
##  [94] Niger                    Nigeria                  Norway                  
##  [97] Oman                     Pakistan                 Panama                  
## [100] Paraguay                 Peru                     Philippines             
## [103] Poland                   Portugal                 Puerto Rico             
## [106] Reunion                  Romania                  Rwanda                  
## [109] Sao Tome and Principe    Saudi Arabia             Senegal                 
## [112] Serbia                   Sierra Leone             Singapore               
## [115] Slovak Republic          Slovenia                 Somalia                 
## [118] South Africa             Spain                    Sri Lanka               
## [121] Sudan                    Swaziland                Sweden                  
## [124] Switzerland              Syria                    Taiwan                  
## [127] Tanzania                 Thailand                 Togo                    
## [130] Trinidad and Tobago      Tunisia                  Turkey                  
## [133] Uganda                   United Kingdom           United States           
## [136] Uruguay                  Venezuela                Vietnam                 
## [139] West Bank and Gaza       Yemen, Rep.              Zambia                  
## [142] Zimbabwe                
## 142 Levels: Afghanistan Albania Algeria Angola Argentina Australia ... Zimbabwe
```


```r
summarise(gapminder, continents = n_distinct(continent))
```

```
## # A tibble: 1 x 1
##   continents
##        <int>
## 1          5
```

```r
unique(gapminder$continent)
```

```
## [1] Asia     Europe   Africa   Americas Oceania 
## Levels: Africa Americas Asia Europe Oceania
```



**8. How many countries are represented on each continent?**

```r
gapminder %>% 
  group_by(continent) %>% 
  summarise(countries = n_distinct(country))
```

```
## # A tibble: 5 x 2
##   continent countries
##   <fct>         <int>
## 1 Africa           52
## 2 Americas         25
## 3 Asia             33
## 4 Europe           30
## 5 Oceania           2
```


**9. For the years included in the data, what is the mean life expectancy by continent? Arrange the results in descending order.**

```r
gapminder %>% 
  group_by(continent) %>% 
  summarise(max_Exp = max(lifeExp),
            min_Exp = min(lifeExp),
            mean_Exp = mean(max_Exp, min_Exp)) %>% 
  arrange(desc(mean_Exp))
```

```
## # A tibble: 5 x 4
##   continent max_Exp min_Exp mean_Exp
##   <fct>       <dbl>   <dbl>    <dbl>
## 1 Asia         82.6    28.8     82.6
## 2 Europe       81.8    43.6     81.8
## 3 Oceania      81.2    69.1     81.2
## 4 Americas     80.7    37.6     80.7
## 5 Africa       76.4    23.6     76.4
```


**10. For the years included in the data, how has life expectancy changed in each country between 1952-2007? How does this look in the USA only?**

```r
difference_gapminder <- 
  gapminder %>% 
  group_by(country) %>%
  filter( year == 1952 | year == 2007) %>% 
  summarise(diff = last(lifeExp)-first(lifeExp))

difference_gapminder
```

```
## # A tibble: 142 x 2
##    country      diff
##    <fct>       <dbl>
##  1 Afghanistan  15.0
##  2 Albania      21.2
##  3 Algeria      29.2
##  4 Angola       12.7
##  5 Argentina    12.8
##  6 Australia    12.1
##  7 Austria      13.0
##  8 Bahrain      24.7
##  9 Bangladesh   26.6
## 10 Belgium      11.4
## # … with 132 more rows
```


```r
difference_gapminder %>% 
  filter(country == "United States")
```

```
## # A tibble: 1 x 2
##   country        diff
##   <fct>         <dbl>
## 1 United States  9.80
```


**11. In the year 2007, which countries had a life expectancy between 70 and 75 years?**

```r
gapminder %>% 
  filter(year == 2007) %>% 
  filter(lifeExp >= 70 & lifeExp <= 75) %>% 
  arrange(desc(lifeExp))
```

```
## # A tibble: 39 x 6
##    country                continent  year lifeExp      pop gdpPercap
##    <fct>                  <fct>     <int>   <dbl>    <int>     <dbl>
##  1 Ecuador                Americas   2007    75.0 13755680     6873.
##  2 Bosnia and Herzegovina Europe     2007    74.9  4552198     7446.
##  3 Slovak Republic        Europe     2007    74.7  5447502    18678.
##  4 Montenegro             Europe     2007    74.5   684736     9254.
##  5 Vietnam                Asia       2007    74.2 85262356     2442.
##  6 Malaysia               Asia       2007    74.2 24821286    12452.
##  7 Syria                  Asia       2007    74.1 19314747     4185.
##  8 Serbia                 Europe     2007    74.0 10150265     9787.
##  9 Libya                  Africa     2007    74.0  6036914    12057.
## 10 Tunisia                Africa     2007    73.9 10276158     7093.
## # … with 29 more rows
```


**10. In 1997, what are the minimum, maximum, and mean life expectancies of the Americas and Europe?**

```r
gapminder %>% 
  filter(year == 1997) %>% 
  filter(continent == "Americas" | continent == "Europe") %>% 
  summarise(minExp = min(lifeExp),
            maxExp  = max(lifeExp),
            meanExp = mean(lifeExp))
```

```
## # A tibble: 1 x 3
##   minExp maxExp meanExp
##    <dbl>  <dbl>   <dbl>
## 1   56.7   79.4    73.5
```


**12. Which countries had the smallest populations in 1952? How about in 2007?**  

```r
gapminder %>% 
  group_by(country) %>% 
  filter(year == 1952) %>% 
  arrange((pop))
```

```
## # A tibble: 142 x 6
## # Groups:   country [142]
##    country               continent  year lifeExp    pop gdpPercap
##    <fct>                 <fct>     <int>   <dbl>  <int>     <dbl>
##  1 Sao Tome and Principe Africa     1952    46.5  60011      880.
##  2 Djibouti              Africa     1952    34.8  63149     2670.
##  3 Bahrain               Asia       1952    50.9 120447     9867.
##  4 Iceland               Europe     1952    72.5 147962     7268.
##  5 Comoros               Africa     1952    40.7 153936     1103.
##  6 Kuwait                Asia       1952    55.6 160000   108382.
##  7 Equatorial Guinea     Africa     1952    34.5 216964      376.
##  8 Reunion               Africa     1952    52.7 257700     2719.
##  9 Gambia                Africa     1952    30   284320      485.
## 10 Swaziland             Africa     1952    41.4 290243     1148.
## # … with 132 more rows
```


```r
gapminder %>% 
  group_by(country) %>% 
  filter(year == 2007) %>% 
  arrange((pop))
```

```
## # A tibble: 142 x 6
## # Groups:   country [142]
##    country               continent  year lifeExp     pop gdpPercap
##    <fct>                 <fct>     <int>   <dbl>   <int>     <dbl>
##  1 Sao Tome and Principe Africa     2007    65.5  199579     1598.
##  2 Iceland               Europe     2007    81.8  301931    36181.
##  3 Djibouti              Africa     2007    54.8  496374     2082.
##  4 Equatorial Guinea     Africa     2007    51.6  551201    12154.
##  5 Montenegro            Europe     2007    74.5  684736     9254.
##  6 Bahrain               Asia       2007    75.6  708573    29796.
##  7 Comoros               Africa     2007    65.2  710960      986.
##  8 Reunion               Africa     2007    76.4  798094     7670.
##  9 Trinidad and Tobago   Americas   2007    69.8 1056608    18009.
## 10 Swaziland             Africa     2007    39.6 1133066     4513.
## # … with 132 more rows
```



**13. We are interested in the GDP for countries in the Middle East including all years in the data. First, separate all of the countries on the "Asia" continent. How many countries are listed and what are their names?**

```r
gapminder %>% 
  filter(continent == "Asia") %>% 
  summarise(countries = n_distinct(country))
```

```
## # A tibble: 1 x 1
##   countries
##       <int>
## 1        33
```


```r
gapminder1 <-  
  gapminder%>% 
  filter(continent == "Asia")

unique(gapminder1$country)
```

```
##  [1] Afghanistan        Bahrain            Bangladesh         Cambodia          
##  [5] China              Hong Kong, China   India              Indonesia         
##  [9] Iran               Iraq               Israel             Japan             
## [13] Jordan             Korea, Dem. Rep.   Korea, Rep.        Kuwait            
## [17] Lebanon            Malaysia           Mongolia           Myanmar           
## [21] Nepal              Oman               Pakistan           Philippines       
## [25] Saudi Arabia       Singapore          Sri Lanka          Syria             
## [29] Taiwan             Thailand           Vietnam            West Bank and Gaza
## [33] Yemen, Rep.       
## 142 Levels: Afghanistan Albania Algeria Angola Argentina Australia ... Zimbabwe
```



**14. Next, remove all of the countries from this list that are part of the Middle East and put them into a new object `gapminder_middleEast`. Add a new column to the data called "region" and make sure "Middle East" is specified for these countries.**

```r
gapminder_middleEast <-
  gapminder1 %>% 
  filter(country == "Afghanistan" | country == "Bahrain" | country == "Iran" | country == "Iraq" | country == "Israel" | country == "Jordan" | country == "Kuwait" | country == "Oman" | country == "Pakistan" | country == "Saudi Arabia" | country == "Syria" | country == "West Bank and Gaza" | country == "Yemen, Rep.") %>% 
  mutate(region = "Middle East ")

gapminder_middleEast
```

```
## # A tibble: 156 x 7
##    country     continent  year lifeExp      pop gdpPercap region        
##    <fct>       <fct>     <int>   <dbl>    <int>     <dbl> <chr>         
##  1 Afghanistan Asia       1952    28.8  8425333      779. "Middle East "
##  2 Afghanistan Asia       1957    30.3  9240934      821. "Middle East "
##  3 Afghanistan Asia       1962    32.0 10267083      853. "Middle East "
##  4 Afghanistan Asia       1967    34.0 11537966      836. "Middle East "
##  5 Afghanistan Asia       1972    36.1 13079460      740. "Middle East "
##  6 Afghanistan Asia       1977    38.4 14880372      786. "Middle East "
##  7 Afghanistan Asia       1982    39.9 12881816      978. "Middle East "
##  8 Afghanistan Asia       1987    40.8 13867957      852. "Middle East "
##  9 Afghanistan Asia       1992    41.7 16317921      649. "Middle East "
## 10 Afghanistan Asia       1997    41.8 22227415      635. "Middle East "
## # … with 146 more rows
```


**15. Now show the gdpPercap for each country with the years as column names; i.e. one row per country.**

```r
gapminder_middleEast %>%
  select(year, country, region, gdpPercap, continent) %>% 
  pivot_wider(names_from = year,
              values_from = gdpPercap)
```

```
## # A tibble: 13 x 15
##    country region continent `1952` `1957` `1962` `1967` `1972` `1977` `1982`
##    <fct>   <chr>  <fct>      <dbl>  <dbl>  <dbl>  <dbl>  <dbl>  <dbl>  <dbl>
##  1 Afghan… "Midd… Asia      7.79e2 8.21e2   853.   836. 7.40e2   786.   978.
##  2 Bahrain "Midd… Asia      9.87e3 1.16e4 12753. 14805. 1.83e4 19340. 19211.
##  3 Iran    "Midd… Asia      3.04e3 3.29e3  4187.  5907. 9.61e3 11889.  7608.
##  4 Iraq    "Midd… Asia      4.13e3 6.23e3  8342.  8931. 9.58e3 14688. 14518.
##  5 Israel  "Midd… Asia      4.09e3 5.39e3  7106.  8394. 1.28e4 13307. 15367.
##  6 Jordan  "Midd… Asia      1.55e3 1.89e3  2348.  2742. 2.11e3  2852.  4161.
##  7 Kuwait  "Midd… Asia      1.08e5 1.14e5 95458. 80895. 1.09e5 59265. 31354.
##  8 Oman    "Midd… Asia      1.83e3 2.24e3  2925.  4721. 1.06e4 11848. 12955.
##  9 Pakist… "Midd… Asia      6.85e2 7.47e2   803.   942. 1.05e3  1176.  1443.
## 10 Saudi … "Midd… Asia      6.46e3 8.16e3 11626. 16903. 2.48e4 34168. 33693.
## 11 Syria   "Midd… Asia      1.64e3 2.12e3  2193.  1882. 2.57e3  3195.  3762.
## 12 West B… "Midd… Asia      1.52e3 1.83e3  2199.  2650. 3.13e3  3683.  4336.
## 13 Yemen,… "Midd… Asia      7.82e2 8.05e2   826.   862. 1.27e3  1830.  1978.
## # … with 5 more variables: `1987` <dbl>, `1992` <dbl>, `1997` <dbl>,
## #   `2002` <dbl>, `2007` <dbl>
```

