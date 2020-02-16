---
title: "HW5"
author: "Priya Bajaj"
date: "2/14/2020"
output: 
  html_document: 
    keep_md: yes
---

```r
##install.packages("naniar")
##install.packages("skimr")
```


```r
library(tidyverse)
```

```
## ── Attaching packages ────────────────────────────────────────────────────────── tidyverse 1.3.0 ──
```

```
## ✓ ggplot2 3.2.1     ✓ purrr   0.3.3
## ✓ tibble  2.1.3     ✓ dplyr   0.8.3
## ✓ tidyr   1.0.2     ✓ stringr 1.4.0
## ✓ readr   1.3.1     ✓ forcats 0.4.0
```

```
## ── Conflicts ───────────────────────────────────────────────────────────── tidyverse_conflicts() ──
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

```r
library(naniar)
library(skimr)
```

```
## 
## Attaching package: 'skimr'
```

```
## The following object is masked from 'package:naniar':
## 
##     n_complete
```


```r
amniota <- 
  readr::read_csv("data/amniota.csv")
```

```
## Parsed with column specification:
## cols(
##   .default = col_double(),
##   class = col_character(),
##   order = col_character(),
##   family = col_character(),
##   genus = col_character(),
##   species = col_character(),
##   common_name = col_character()
## )
```

```
## See spec(...) for full column specifications.
```


```r
amphibio <- 
  readr::read_csv("data/amphibio.csv")
```

```
## Parsed with column specification:
## cols(
##   .default = col_double(),
##   id = col_character(),
##   Order = col_character(),
##   Family = col_character(),
##   Genus = col_character(),
##   Species = col_character(),
##   Seeds = col_logical(),
##   OBS = col_logical()
## )
```

```
## See spec(...) for full column specifications.
```

```
## Warning: 125 parsing failures.
##  row col           expected                                                           actual                file
## 1410 OBS 1/0/T/F/TRUE/FALSE Identified as P. appendiculata in Boquimpani-Freitas et al. 2002 'data/amphibio.csv'
## 1416 OBS 1/0/T/F/TRUE/FALSE Identified as T. miliaris in Giaretta and Facure 2004            'data/amphibio.csv'
## 1447 OBS 1/0/T/F/TRUE/FALSE Considered endangered by Soto-Azat et al. 2013                   'data/amphibio.csv'
## 1448 OBS 1/0/T/F/TRUE/FALSE Considered extinct by Soto-Azat et al. 2013                      'data/amphibio.csv'
## 1471 OBS 1/0/T/F/TRUE/FALSE nomem dubitum                                                    'data/amphibio.csv'
## .... ... .................. ................................................................ ...................
## See problems(...) for more details.
```


```r
str(amphibio)
```

```
## Classes 'spec_tbl_df', 'tbl_df', 'tbl' and 'data.frame':	6776 obs. of  38 variables:
##  $ id                     : chr  "Anf0001" "Anf0002" "Anf0003" "Anf0004" ...
##  $ Order                  : chr  "Anura" "Anura" "Anura" "Anura" ...
##  $ Family                 : chr  "Allophrynidae" "Alytidae" "Alytidae" "Alytidae" ...
##  $ Genus                  : chr  "Allophryne" "Alytes" "Alytes" "Alytes" ...
##  $ Species                : chr  "Allophryne ruthveni" "Alytes cisternasii" "Alytes dickhilleni" "Alytes maurus" ...
##  $ Fos                    : num  NA NA NA NA NA 1 1 1 1 1 ...
##  $ Ter                    : num  1 1 1 1 1 1 1 1 1 1 ...
##  $ Aqu                    : num  1 1 1 1 NA 1 1 1 1 1 ...
##  $ Arb                    : num  1 1 1 1 1 1 NA NA NA NA ...
##  $ Leaves                 : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ Flowers                : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ Seeds                  : logi  NA NA NA NA NA NA ...
##  $ Fruits                 : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ Arthro                 : num  1 1 1 NA 1 1 1 1 1 NA ...
##  $ Vert                   : num  NA NA NA NA NA NA 1 NA NA NA ...
##  $ Diu                    : num  1 NA NA NA NA NA 1 1 1 NA ...
##  $ Noc                    : num  1 1 1 NA 1 1 1 1 1 NA ...
##  $ Crepu                  : num  1 NA NA NA NA 1 NA NA NA NA ...
##  $ Wet_warm               : num  NA NA NA NA 1 1 NA NA NA NA ...
##  $ Wet_cold               : num  1 NA NA NA NA NA 1 NA NA NA ...
##  $ Dry_warm               : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ Dry_cold               : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ Body_mass_g            : num  31 6.1 NA NA 2.31 13.4 21.8 NA NA NA ...
##  $ Age_at_maturity_min_y  : num  NA 2 2 NA 3 2 3 NA NA NA ...
##  $ Age_at_maturity_max_y  : num  NA 2 2 NA 3 3 5 NA NA NA ...
##  $ Body_size_mm           : num  31 50 55 NA 40 55 80 60 65 NA ...
##  $ Size_at_maturity_min_mm: num  NA 27 NA NA NA 35 NA NA NA NA ...
##  $ Size_at_maturity_max_mm: num  NA 36 NA NA NA 40.5 NA NA NA NA ...
##  $ Longevity_max_y        : num  NA 6 NA NA NA 7 9 NA NA NA ...
##  $ Litter_size_min_n      : num  300 60 40 NA 7 53 300 1500 1000 NA ...
##  $ Litter_size_max_n      : num  300 180 40 NA 20 171 1500 1500 1000 NA ...
##  $ Reproductive_output_y  : num  1 4 1 4 1 4 6 1 1 1 ...
##  $ Offspring_size_min_mm  : num  NA 2.6 NA NA 5.4 2.6 1.5 NA 1.5 NA ...
##  $ Offspring_size_max_mm  : num  NA 3.5 NA NA 7 5 2 NA 1.5 NA ...
##  $ Dir                    : num  0 0 0 0 0 0 0 0 0 0 ...
##  $ Lar                    : num  1 1 1 1 1 1 1 1 1 1 ...
##  $ Viv                    : num  0 0 0 0 0 0 0 0 0 0 ...
##  $ OBS                    : logi  NA NA NA NA NA NA ...
##  - attr(*, "problems")=Classes 'tbl_df', 'tbl' and 'data.frame':	125 obs. of  5 variables:
##   ..$ row     : int  1410 1416 1447 1448 1471 1488 1539 1540 1543 1544 ...
##   ..$ col     : chr  "OBS" "OBS" "OBS" "OBS" ...
##   ..$ expected: chr  "1/0/T/F/TRUE/FALSE" "1/0/T/F/TRUE/FALSE" "1/0/T/F/TRUE/FALSE" "1/0/T/F/TRUE/FALSE" ...
##   ..$ actual  : chr  "Identified as P. appendiculata in Boquimpani-Freitas et al. 2002" "Identified as T. miliaris in Giaretta and Facure 2004" "Considered endangered by Soto-Azat et al. 2013" "Considered extinct by Soto-Azat et al. 2013" ...
##   ..$ file    : chr  "'data/amphibio.csv'" "'data/amphibio.csv'" "'data/amphibio.csv'" "'data/amphibio.csv'" ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   id = col_character(),
##   ..   Order = col_character(),
##   ..   Family = col_character(),
##   ..   Genus = col_character(),
##   ..   Species = col_character(),
##   ..   Fos = col_double(),
##   ..   Ter = col_double(),
##   ..   Aqu = col_double(),
##   ..   Arb = col_double(),
##   ..   Leaves = col_double(),
##   ..   Flowers = col_double(),
##   ..   Seeds = col_logical(),
##   ..   Fruits = col_double(),
##   ..   Arthro = col_double(),
##   ..   Vert = col_double(),
##   ..   Diu = col_double(),
##   ..   Noc = col_double(),
##   ..   Crepu = col_double(),
##   ..   Wet_warm = col_double(),
##   ..   Wet_cold = col_double(),
##   ..   Dry_warm = col_double(),
##   ..   Dry_cold = col_double(),
##   ..   Body_mass_g = col_double(),
##   ..   Age_at_maturity_min_y = col_double(),
##   ..   Age_at_maturity_max_y = col_double(),
##   ..   Body_size_mm = col_double(),
##   ..   Size_at_maturity_min_mm = col_double(),
##   ..   Size_at_maturity_max_mm = col_double(),
##   ..   Longevity_max_y = col_double(),
##   ..   Litter_size_min_n = col_double(),
##   ..   Litter_size_max_n = col_double(),
##   ..   Reproductive_output_y = col_double(),
##   ..   Offspring_size_min_mm = col_double(),
##   ..   Offspring_size_max_mm = col_double(),
##   ..   Dir = col_double(),
##   ..   Lar = col_double(),
##   ..   Viv = col_double(),
##   ..   OBS = col_logical()
##   .. )
```


```r
colnames(amphibio)
```

```
##  [1] "id"                      "Order"                  
##  [3] "Family"                  "Genus"                  
##  [5] "Species"                 "Fos"                    
##  [7] "Ter"                     "Aqu"                    
##  [9] "Arb"                     "Leaves"                 
## [11] "Flowers"                 "Seeds"                  
## [13] "Fruits"                  "Arthro"                 
## [15] "Vert"                    "Diu"                    
## [17] "Noc"                     "Crepu"                  
## [19] "Wet_warm"                "Wet_cold"               
## [21] "Dry_warm"                "Dry_cold"               
## [23] "Body_mass_g"             "Age_at_maturity_min_y"  
## [25] "Age_at_maturity_max_y"   "Body_size_mm"           
## [27] "Size_at_maturity_min_mm" "Size_at_maturity_max_mm"
## [29] "Longevity_max_y"         "Litter_size_min_n"      
## [31] "Litter_size_max_n"       "Reproductive_output_y"  
## [33] "Offspring_size_min_mm"   "Offspring_size_max_mm"  
## [35] "Dir"                     "Lar"                    
## [37] "Viv"                     "OBS"
```


```r
dim(amphibio)
```

```
## [1] 6776   38
```


```r
str(amniota)
```

```
## Classes 'spec_tbl_df', 'tbl_df', 'tbl' and 'data.frame':	21322 obs. of  36 variables:
##  $ class                                : chr  "Aves" "Aves" "Aves" "Aves" ...
##  $ order                                : chr  "Accipitriformes" "Accipitriformes" "Accipitriformes" "Accipitriformes" ...
##  $ family                               : chr  "Accipitridae" "Accipitridae" "Accipitridae" "Accipitridae" ...
##  $ genus                                : chr  "Accipiter" "Accipiter" "Accipiter" "Accipiter" ...
##  $ species                              : chr  "albogularis" "badius" "bicolor" "brachyurus" ...
##  $ subspecies                           : num  -999 -999 -999 -999 -999 -999 -999 -999 -999 -999 ...
##  $ common_name                          : chr  "Pied Goshawk" "Shikra" "Bicolored Hawk" "New Britain Sparrowhawk" ...
##  $ female_maturity_d                    : num  -999 363 -999 -999 363 ...
##  $ litter_or_clutch_size_n              : num  -999 3.25 2.7 -999 4 -999 2.7 4.25 3.25 4.35 ...
##  $ litters_or_clutches_per_y            : num  -999 1 -999 -999 1 -999 -999 1 -999 1 ...
##  $ adult_body_mass_g                    : num  252 140 345 142 204 ...
##  $ maximum_longevity_y                  : num  -999 -999 -999 -999 -999 ...
##  $ gestation_d                          : num  -999 -999 -999 -999 -999 -999 -999 -999 -999 -999 ...
##  $ weaning_d                            : num  -999 -999 -999 -999 -999 -999 -999 -999 -999 -999 ...
##  $ birth_or_hatching_weight_g           : num  -999 -999 -999 -999 -999 -999 -999 -999 -999 28 ...
##  $ weaning_weight_g                     : num  -999 -999 -999 -999 -999 -999 -999 -999 -999 -999 ...
##  $ egg_mass_g                           : num  -999 21 32 -999 21.9 ...
##  $ incubation_d                         : num  -999 30 -999 -999 32.5 ...
##  $ fledging_age_d                       : num  -999 32 -999 -999 42.5 ...
##  $ longevity_y                          : num  -999 -999 -999 -999 -999 ...
##  $ male_maturity_d                      : num  -999 -999 -999 -999 -999 -999 -999 365 -999 730 ...
##  $ inter_litter_or_interbirth_interval_y: num  -999 -999 -999 -999 -999 -999 -999 -999 -999 -999 ...
##  $ female_body_mass_g                   : num  352 168 390 -999 230 ...
##  $ male_body_mass_g                     : num  223 125 212 142 170 ...
##  $ no_sex_body_mass_g                   : num  -999 123 -999 -999 -999 ...
##  $ egg_width_mm                         : num  -999 -999 -999 -999 -999 -999 -999 -999 -999 -999 ...
##  $ egg_length_mm                        : num  -999 -999 -999 -999 -999 -999 -999 -999 -999 -999 ...
##  $ fledging_mass_g                      : num  -999 -999 -999 -999 -999 -999 -999 -999 -999 -999 ...
##  $ adult_svl_cm                         : num  -999 30 39.5 -999 33.5 -999 39.5 29 32.5 42 ...
##  $ male_svl_cm                          : num  -999 -999 -999 -999 -999 -999 -999 -999 -999 -999 ...
##  $ female_svl_cm                        : num  -999 -999 -999 -999 -999 -999 -999 -999 -999 -999 ...
##  $ birth_or_hatching_svl_cm             : num  -999 -999 -999 -999 -999 -999 -999 -999 -999 -999 ...
##  $ female_svl_at_maturity_cm            : num  -999 -999 -999 -999 -999 -999 -999 -999 -999 -999 ...
##  $ female_body_mass_at_maturity_g       : num  -999 -999 -999 -999 -999 -999 -999 -999 -999 -999 ...
##  $ no_sex_svl_cm                        : num  -999 -999 -999 -999 -999 -999 -999 -999 -999 -999 ...
##  $ no_sex_maturity_d                    : num  -999 -999 -999 -999 -999 -999 -999 -999 -999 -999 ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   class = col_character(),
##   ..   order = col_character(),
##   ..   family = col_character(),
##   ..   genus = col_character(),
##   ..   species = col_character(),
##   ..   subspecies = col_double(),
##   ..   common_name = col_character(),
##   ..   female_maturity_d = col_double(),
##   ..   litter_or_clutch_size_n = col_double(),
##   ..   litters_or_clutches_per_y = col_double(),
##   ..   adult_body_mass_g = col_double(),
##   ..   maximum_longevity_y = col_double(),
##   ..   gestation_d = col_double(),
##   ..   weaning_d = col_double(),
##   ..   birth_or_hatching_weight_g = col_double(),
##   ..   weaning_weight_g = col_double(),
##   ..   egg_mass_g = col_double(),
##   ..   incubation_d = col_double(),
##   ..   fledging_age_d = col_double(),
##   ..   longevity_y = col_double(),
##   ..   male_maturity_d = col_double(),
##   ..   inter_litter_or_interbirth_interval_y = col_double(),
##   ..   female_body_mass_g = col_double(),
##   ..   male_body_mass_g = col_double(),
##   ..   no_sex_body_mass_g = col_double(),
##   ..   egg_width_mm = col_double(),
##   ..   egg_length_mm = col_double(),
##   ..   fledging_mass_g = col_double(),
##   ..   adult_svl_cm = col_double(),
##   ..   male_svl_cm = col_double(),
##   ..   female_svl_cm = col_double(),
##   ..   birth_or_hatching_svl_cm = col_double(),
##   ..   female_svl_at_maturity_cm = col_double(),
##   ..   female_body_mass_at_maturity_g = col_double(),
##   ..   no_sex_svl_cm = col_double(),
##   ..   no_sex_maturity_d = col_double()
##   .. )
```


```r
colnames(amniota)
```

```
##  [1] "class"                                
##  [2] "order"                                
##  [3] "family"                               
##  [4] "genus"                                
##  [5] "species"                              
##  [6] "subspecies"                           
##  [7] "common_name"                          
##  [8] "female_maturity_d"                    
##  [9] "litter_or_clutch_size_n"              
## [10] "litters_or_clutches_per_y"            
## [11] "adult_body_mass_g"                    
## [12] "maximum_longevity_y"                  
## [13] "gestation_d"                          
## [14] "weaning_d"                            
## [15] "birth_or_hatching_weight_g"           
## [16] "weaning_weight_g"                     
## [17] "egg_mass_g"                           
## [18] "incubation_d"                         
## [19] "fledging_age_d"                       
## [20] "longevity_y"                          
## [21] "male_maturity_d"                      
## [22] "inter_litter_or_interbirth_interval_y"
## [23] "female_body_mass_g"                   
## [24] "male_body_mass_g"                     
## [25] "no_sex_body_mass_g"                   
## [26] "egg_width_mm"                         
## [27] "egg_length_mm"                        
## [28] "fledging_mass_g"                      
## [29] "adult_svl_cm"                         
## [30] "male_svl_cm"                          
## [31] "female_svl_cm"                        
## [32] "birth_or_hatching_svl_cm"             
## [33] "female_svl_at_maturity_cm"            
## [34] "female_body_mass_at_maturity_g"       
## [35] "no_sex_svl_cm"                        
## [36] "no_sex_maturity_d"
```


```r
dim(amniota)
```

```
## [1] 21322    36
```

####NAs are represented by -999


```r
amniota %>% 
  summarize(total_na = sum(is.na(amniota)))
```

```
## # A tibble: 1 x 1
##   total_na
##      <int>
## 1        0
```

```r
amphibio %>% 
  summarize(total_nas = sum(is.na(amphibio)))
```

```
## # A tibble: 1 x 1
##   total_nas
##       <int>
## 1    170691
```


```r
amniota2 <- 
  amniota %>% 
  na_if("-999")
amniota2
```

```
## # A tibble: 21,322 x 36
##    class order family genus species subspecies common_name female_maturity…
##    <chr> <chr> <chr>  <chr> <chr>        <dbl> <chr>                  <dbl>
##  1 Aves  Acci… Accip… Acci… albogu…         NA Pied Gosha…              NA 
##  2 Aves  Acci… Accip… Acci… badius          NA Shikra                  363.
##  3 Aves  Acci… Accip… Acci… bicolor         NA Bicolored …              NA 
##  4 Aves  Acci… Accip… Acci… brachy…         NA New Britai…              NA 
##  5 Aves  Acci… Accip… Acci… brevip…         NA Levant Spa…             363.
##  6 Aves  Acci… Accip… Acci… castan…         NA Chestnut-f…              NA 
##  7 Aves  Acci… Accip… Acci… chilen…         NA Chilean Ha…              NA 
##  8 Aves  Acci… Accip… Acci… chiono…         NA White-brea…             548.
##  9 Aves  Acci… Accip… Acci… cirroc…         NA Collared S…              NA 
## 10 Aves  Acci… Accip… Acci… cooper…         NA Cooper's H…             730 
## # … with 21,312 more rows, and 28 more variables:
## #   litter_or_clutch_size_n <dbl>, litters_or_clutches_per_y <dbl>,
## #   adult_body_mass_g <dbl>, maximum_longevity_y <dbl>, gestation_d <dbl>,
## #   weaning_d <dbl>, birth_or_hatching_weight_g <dbl>, weaning_weight_g <dbl>,
## #   egg_mass_g <dbl>, incubation_d <dbl>, fledging_age_d <dbl>,
## #   longevity_y <dbl>, male_maturity_d <dbl>,
## #   inter_litter_or_interbirth_interval_y <dbl>, female_body_mass_g <dbl>,
## #   male_body_mass_g <dbl>, no_sex_body_mass_g <dbl>, egg_width_mm <dbl>,
## #   egg_length_mm <dbl>, fledging_mass_g <dbl>, adult_svl_cm <dbl>,
## #   male_svl_cm <dbl>, female_svl_cm <dbl>, birth_or_hatching_svl_cm <dbl>,
## #   female_svl_at_maturity_cm <dbl>, female_body_mass_at_maturity_g <dbl>,
## #   no_sex_svl_cm <dbl>, no_sex_maturity_d <dbl>
```


```r
amphibio2 <- 
  amphibio %>% 
  na_if("-999")
amphibio2
```

```
## # A tibble: 6,776 x 38
##    id    Order Family Genus Species   Fos   Ter   Aqu   Arb Leaves Flowers Seeds
##    <chr> <chr> <chr>  <chr> <chr>   <dbl> <dbl> <dbl> <dbl>  <dbl>   <dbl> <lgl>
##  1 Anf0… Anura Allop… Allo… Alloph…    NA     1     1     1     NA      NA NA   
##  2 Anf0… Anura Alyti… Alyt… Alytes…    NA     1     1     1     NA      NA NA   
##  3 Anf0… Anura Alyti… Alyt… Alytes…    NA     1     1     1     NA      NA NA   
##  4 Anf0… Anura Alyti… Alyt… Alytes…    NA     1     1     1     NA      NA NA   
##  5 Anf0… Anura Alyti… Alyt… Alytes…    NA     1    NA     1     NA      NA NA   
##  6 Anf0… Anura Alyti… Alyt… Alytes…     1     1     1     1     NA      NA NA   
##  7 Anf0… Anura Alyti… Disc… Discog…     1     1     1    NA     NA      NA NA   
##  8 Anf0… Anura Alyti… Disc… Discog…     1     1     1    NA     NA      NA NA   
##  9 Anf0… Anura Alyti… Disc… Discog…     1     1     1    NA     NA      NA NA   
## 10 Anf0… Anura Alyti… Disc… Discog…     1     1     1    NA     NA      NA NA   
## # … with 6,766 more rows, and 26 more variables: Fruits <dbl>, Arthro <dbl>,
## #   Vert <dbl>, Diu <dbl>, Noc <dbl>, Crepu <dbl>, Wet_warm <dbl>,
## #   Wet_cold <dbl>, Dry_warm <dbl>, Dry_cold <dbl>, Body_mass_g <dbl>,
## #   Age_at_maturity_min_y <dbl>, Age_at_maturity_max_y <dbl>,
## #   Body_size_mm <dbl>, Size_at_maturity_min_mm <dbl>,
## #   Size_at_maturity_max_mm <dbl>, Longevity_max_y <dbl>,
## #   Litter_size_min_n <dbl>, Litter_size_max_n <dbl>,
## #   Reproductive_output_y <dbl>, Offspring_size_min_mm <dbl>,
## #   Offspring_size_max_mm <dbl>, Dir <dbl>, Lar <dbl>, Viv <dbl>, OBS <lgl>
```


```r
naniar::miss_var_summary(amniota2)
```

```
## # A tibble: 36 x 3
##    variable                       n_miss pct_miss
##    <chr>                           <int>    <dbl>
##  1 subspecies                      21322    100  
##  2 female_body_mass_at_maturity_g  21318    100. 
##  3 female_svl_at_maturity_cm       21120     99.1
##  4 fledging_mass_g                 21111     99.0
##  5 male_svl_cm                     21040     98.7
##  6 no_sex_maturity_d               20860     97.8
##  7 egg_width_mm                    20727     97.2
##  8 egg_length_mm                   20702     97.1
##  9 weaning_weight_g                20258     95.0
## 10 female_svl_cm                   20242     94.9
## # … with 26 more rows
```


```r
naniar::miss_var_summary(amphibio2)
```

```
## # A tibble: 38 x 3
##    variable n_miss pct_miss
##    <chr>     <int>    <dbl>
##  1 OBS        6776    100  
##  2 Fruits     6774    100. 
##  3 Flowers    6772     99.9
##  4 Seeds      6772     99.9
##  5 Leaves     6752     99.6
##  6 Dry_cold   6735     99.4
##  7 Vert       6657     98.2
##  8 Wet_cold   6625     97.8
##  9 Crepu      6608     97.5
## 10 Dry_warm   6572     97.0
## # … with 28 more rows
```


```r
amniota2 %>% 
  group_by(class) %>% 
  select(class,egg_mass_g) %>% 
  summarise(total_Na = sum(is.na(egg_mass_g)))
```

```
## # A tibble: 3 x 2
##   class    total_Na
##   <chr>       <int>
## 1 Aves         4914
## 2 Mammalia     4953
## 3 Reptilia     6040
```
##It makes sense to have NAs as most mammals don't lay eggs. It's surprising to have missing information for reptiles however.


```r
amniota2 %>%
  group_by(class) %>% 
  ggplot(aes(x = class)) +
  geom_bar(stat = "count")
```

![](HW5_files/figure-html/unnamed-chunk-18-1.png)<!-- -->


```r
amniota2 %>% 
  group_by(class) %>% 
  summarise(Total_Genera = n_distinct(genus))
```

```
## # A tibble: 3 x 2
##   class    Total_Genera
##   <chr>           <int>
## 1 Aves             2169
## 2 Mammalia         1200
## 3 Reptilia          967
```


```r
amniota2 %>%
  group_by(class) %>% 
  summarise(Total_Genera = n_distinct(genus)) %>% 
  ggplot(aes(x = class, y = Total_Genera))+
  geom_bar(stat = "identity")
```

![](HW5_files/figure-html/unnamed-chunk-20-1.png)<!-- -->


```r
amniota2 %>% 
  group_by(class) %>% 
  summarise(Total_Species = n_distinct(species))
```

```
## # A tibble: 3 x 2
##   class    Total_Species
##   <chr>            <int>
## 1 Aves              5525
## 2 Mammalia          3473
## 3 Reptilia          4692
```


```r
amniota2 %>%
  group_by(class) %>% 
  summarise(Total_Species = n_distinct(species)) %>% 
  ggplot(aes(x = class, y = Total_Species))+
  geom_bar(stat = "identity")
```

![](HW5_files/figure-html/unnamed-chunk-22-1.png)<!-- -->


```r
amphibio2 %>% 
  pivot_longer(Fos:Arb,
               names_to = "Ecology",
               values_to = "Count") %>% 
  group_by(Ecology) %>% 
  summarise(species_numbers = sum(Count, na.rm = T)) %>%
  ggplot(aes(x = Ecology, y = species_numbers))+
  geom_bar(stat = "identity")
```

![](HW5_files/figure-html/unnamed-chunk-23-1.png)<!-- -->


```r
amphibio2 %>% 
  ggplot(aes(x = Body_size_mm, y = Litter_size_min_n))+
  geom_point(na.rm = T)+
  geom_smooth(method = lm)
```

```
## Warning: Removed 5181 rows containing non-finite values (stat_smooth).
```

![](HW5_files/figure-html/unnamed-chunk-24-1.png)<!-- -->
