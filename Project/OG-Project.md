---
title: "Bis15 Project"
author: "Priya Bajaj"
date: "2/28/2020"
output: 
  html_document: 
    keep_md: yes
---


```r
library("tidyverse")
```

```
## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.0 ──
```

```
## ✓ ggplot2 3.2.1     ✓ purrr   0.3.3
## ✓ tibble  2.1.3     ✓ dplyr   0.8.4
## ✓ tidyr   1.0.2     ✓ stringr 1.4.0
## ✓ readr   1.3.1     ✓ forcats 0.4.0
```

```
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

Read Data

```r
data <- readr::read_csv("~/Desktop/BIS15W2020_PBajaj_Project-master/Project/test.csv")
```

```
## Warning: Missing column names filled in: 'X1' [1], 'X3' [3], 'X4' [4], 'X5' [5],
## 'X6' [6], 'X7' [7], 'X9' [9], 'X10' [10], 'X11' [11], 'X13' [13], 'X14' [14],
## 'X15' [15], 'X16' [16], 'X17' [17], 'X18' [18], 'X19' [19], 'X20' [20]
```

```
## Parsed with column specification:
## cols(
##   .default = col_character(),
##   X3 = col_logical(),
##   X5 = col_logical(),
##   X7 = col_logical(),
##   X9 = col_logical(),
##   X11 = col_logical(),
##   X13 = col_logical(),
##   X15 = col_logical(),
##   X17 = col_logical(),
##   X19 = col_logical()
## )
```

```
## See spec(...) for full column specifications.
```

Select Out empty rows

```r
data2 <- data[-c(1,2,3,4,5,8,20,21,25,28,31,34,35,36,37,38,39,40,41,42,43,50,51,52,53,54,55,56,57,63,64,65,66,67,68,69,70,71,72), ]
```

Select Out Empty Columns

```r
df = subset(data2, select = -c(X3,X5,X7,X9,X11,X13,X15,X17,X19) )
```

Renmae Columns

```r
data3 <- df %>% 
  rename(Characteristics= "X1", Activity_Reduction="ROLE EMOTIONAL SCALE", Less_Accomplished="X4", Less_Careful_Work= "X6", Physical_Emotional_Health_VS_Social= "SOCIAL FUNCTIONING SCALE", Health_VS_SocialAct.="X10", Nervousness= "MENTAL HEALTH SCALE", Un_Cheerable="X14", Calm="X16",Downhearted="X18", Happy="X20")
```

Separate values into observations and totals.

```r
data4 <- data3 %>% 
  separate(Activity_Reduction, into= c("Activity Reduction", "TotalPop"),  sep = "/")  %>% 
  separate(Less_Accomplished, into = c("Less Accomplished", "TotalPop2"), sep = "/")  %>% 
  separate(Less_Careful_Work, into = c("Less Careful Work", "TotalPop3"), sep = "/")  %>%
  separate(Physical_Emotional_Health_VS_Social, into = c("Phys_Emotional Prob Affectting Social Activity", "TotalPop4"), sep = "/")    %>% 
  separate(Health_VS_SocialAct., into = c("Health limits Social Act", "TotalPop5"), sep = "/")   %>% 
  separate(Nervousness, into = c("Nervousness", "TotalPop6"), sep = "/")   %>% 
  separate(Un_Cheerable, into = c("Uncheerable", "TotaPop7"), sep = "/")   %>% 
  separate(Calm, into = c("Calm", "TotalPop8"),sep = "/")      %>% 
  separate(Downhearted, into = c("Downhearted", "TotalPop9"), sep = "/") %>% 
  separate(Happy, into = c("Happy", "TotalPop10"), sep = "/")
data4
```

```
## # A tibble: 33 x 21
##    Characteristics `Activity Reduc… TotalPop `Less Accomplis… TotalPop2
##    <chr>           <chr>            <chr>    <chr>            <chr>    
##  1 Male            610              5222 (1… 903              5221 (17…
##  2 Female          846              4999 (1… 1155             4996 (23…
##  3 Leukemia        321              2811 (1… 478              2812 (17…
##  4 Hodgkin         93               732 (12… 132              730 (18.…
##  5 NHL             75               527 (14… 110              530 (20.…
##  6 CNS             437              2153 (2… 585              2153 (27…
##  7 Neuroblastoma   55               424 (13… 79               425 (18.…
##  8 Non-Heritable … 47               407 (11… 69               405 (17.…
##  9 Heritable Reti… 43               288 (14… 68               290 (23.…
## 10 Wilms           119              939 (12… 153              935 (16.…
## # … with 23 more rows, and 16 more variables: `Less Careful Work` <chr>,
## #   TotalPop3 <chr>, `Phys_Emotional Prob Affectting Social Activity` <chr>,
## #   TotalPop4 <chr>, `Health limits Social Act` <chr>, TotalPop5 <chr>,
## #   Nervousness <chr>, TotalPop6 <chr>, Uncheerable <chr>, TotaPop7 <chr>,
## #   Calm <chr>, TotalPop8 <chr>, Downhearted <chr>, TotalPop9 <chr>,
## #   Happy <chr>, TotalPop10 <chr>
```

Remove the percentages from the total columns.

```r
data5 <- data4   %>% 
  separate(TotalPop, into = c("TotalPop1", "% Reported1"), sep = " ")  %>% 
  separate(TotalPop2, into = c("TotalPop2", "% Reported2"), sep = " ")  %>% 
  separate(TotalPop3, into = c("TotalPop3", "% Reported3"), sep = " ")  %>% 
  separate(TotalPop4, into = c("TotalPop4", "% Reported4"), sep = " ")  %>% 
  separate(TotalPop5, into = c("TotalPop5", "% Reported5"), sep = " ")  %>% 
  separate(TotalPop6, into = c("TotalPop6", "% Reported6"), sep = " ")  %>% 
  separate(TotaPop7, into = c("TotalPop7", "% Reported7"), sep = " ")  %>% 
  separate(TotalPop8, into = c("TotalPop8", "% Reported8"), sep = " ")  %>% 
  separate(TotalPop9, into = c("TotalPop9", "% Reported9"), sep = " ")  %>% 
  separate(TotalPop10, into = c("TotalPop10", "% Reported10"), sep = " ")
data5
```

```
## # A tibble: 33 x 31
##    Characteristics `Activity Reduc… TotalPop1 `% Reported1` `Less Accomplis…
##    <chr>           <chr>            <chr>     <chr>         <chr>           
##  1 Male            610              5222      (11.7)        903             
##  2 Female          846              4999      (16.9)        1155            
##  3 Leukemia        321              2811      (11.4)        478             
##  4 Hodgkin         93               732       (12.7)        132             
##  5 NHL             75               527       (14.2)        110             
##  6 CNS             437              2153      (20.3)        585             
##  7 Neuroblastoma   55               424       (13.0)        79              
##  8 Non-Heritable … 47               407       (11.6)        69              
##  9 Heritable Reti… 43               288       (14.9)        68              
## 10 Wilms           119              939       (12.7)        153             
## # … with 23 more rows, and 26 more variables: TotalPop2 <chr>, `%
## #   Reported2` <chr>, `Less Careful Work` <chr>, TotalPop3 <chr>, `%
## #   Reported3` <chr>, `Phys_Emotional Prob Affectting Social Activity` <chr>,
## #   TotalPop4 <chr>, `% Reported4` <chr>, `Health limits Social Act` <chr>,
## #   TotalPop5 <chr>, `% Reported5` <chr>, Nervousness <chr>, TotalPop6 <chr>,
## #   `% Reported6` <chr>, Uncheerable <chr>, TotalPop7 <chr>, `%
## #   Reported7` <chr>, Calm <chr>, TotalPop8 <chr>, `% Reported8` <chr>,
## #   Downhearted <chr>, TotalPop9 <chr>, `% Reported9` <chr>, Happy <chr>,
## #   TotalPop10 <chr>, `% Reported10` <chr>
```


```r
glimpse(data5)
```

```
## Observations: 33
## Variables: 31
## $ Characteristics                                  <chr> "Male", "Female", "L…
## $ `Activity Reduction`                             <chr> "610", "846", "321",…
## $ TotalPop1                                        <chr> "5222", "4999", "281…
## $ `% Reported1`                                    <chr> "(11.7)", "(16.9)", …
## $ `Less Accomplished`                              <chr> "903", "1155", "478"…
## $ TotalPop2                                        <chr> "5221", "4996", "281…
## $ `% Reported2`                                    <chr> "(17.3)", "(23.1)", …
## $ `Less Careful Work`                              <chr> "670", "934", "368",…
## $ TotalPop3                                        <chr> "5212", "4974", "280…
## $ `% Reported3`                                    <chr> "(12.9)", "(18.8)", …
## $ `Phys_Emotional Prob Affectting Social Activity` <chr> "796", "1022", "410"…
## $ TotalPop4                                        <chr> "5300", "5081", "285…
## $ `% Reported4`                                    <chr> "(15.0)", "(20.1)", …
## $ `Health limits Social Act`                       <chr> "847", "1075", "374"…
## $ TotalPop5                                        <chr> "5249", "5026", "282…
## $ `% Reported5`                                    <chr> "(16.1)", "(21.4)", …
## $ Nervousness                                      <chr> "1328", "1626", "848…
## $ TotalPop6                                        <chr> "5271", "5065", "283…
## $ `% Reported6`                                    <chr> "(25.2)", "(32.1)", …
## $ Uncheerable                                      <chr> "1018", "1425", "686…
## $ TotalPop7                                        <chr> "5279", "5064", "284…
## $ `% Reported7`                                    <chr> "(19.3)", "(28.1)", …
## $ Calm                                             <chr> "2000", "2527", "119…
## $ TotalPop8                                        <chr> "5278", "5062", "283…
## $ `% Reported8`                                    <chr> "(37.9)", "(49.9)", …
## $ Downhearted                                      <chr> "1530", "1975", "977…
## $ TotalPop9                                        <chr> "5258", "5050", "282…
## $ `% Reported9`                                    <chr> "(29.1)", "(39.1)", …
## $ Happy                                            <chr> "1139", "1283", "559…
## $ TotalPop10                                       <chr> "5274", "5065", "283…
## $ `% Reported10`                                   <chr> "(21.6)", "(25.3)", …
```



```r
 data_subset <- data5 %>% 
  select(Characteristics,`Activity Reduction`, `Less Accomplished`, `Phys_Emotional Prob Affectting Social Activity`, `Nervousness`, `Uncheerable`, `Calm`, `Downhearted`,`Happy` ) %>% 
  filter(Characteristics== "Male" | Characteristics == "Female" |Characteristics == "Leukemia" | Characteristics== "Hodgkin"| Characteristics== "NHL"|Characteristics== "CNS" | Characteristics== "Neuroblastoma" |  Characteristics=="Non-Heritable Retinoblastoma" | Characteristics=="Heritable Retinoblastoma" |Characteristics=="Wilms" | Characteristics== "Bone Sarcoma" | Characteristics == "Soft Tissue Sarcoma" | Characteristics=="Other"| Characteristics=="0-4 years" | Characteristics== "5-9 years" | Characteristics== "10-14 years" | Characteristics=="No" | Characteristics== "Yes" | Characteristics == "Single" | Characteristics=="Married" | Characteristics=="Separated" | Characteristics== "Divorced" | Characteristics== "Widowed" | Characteristics== "Student" | Characteristics== "Never worked/Unemployed" | Characteristics== "Routine/Manual" | Characteristics== "Intermediate" | Characteristics=="Managerial/Professional")
```

Select Male and Female From characteristics

```r
plot1 <- data_subset %>% 
  filter(Characteristics=="Male" | Characteristics=="Female") %>% 
  pivot_longer(-Characteristics,
               names_to = "em_state",
               values_to = "count")

plot1$count <- as.numeric(plot1$count)
plot1
```

```
## # A tibble: 16 x 3
##    Characteristics em_state                                       count
##    <chr>           <chr>                                          <dbl>
##  1 Male            Activity Reduction                               610
##  2 Male            Less Accomplished                                903
##  3 Male            Phys_Emotional Prob Affectting Social Activity   796
##  4 Male            Nervousness                                     1328
##  5 Male            Uncheerable                                     1018
##  6 Male            Calm                                            2000
##  7 Male            Downhearted                                     1530
##  8 Male            Happy                                           1139
##  9 Female          Activity Reduction                               846
## 10 Female          Less Accomplished                               1155
## 11 Female          Phys_Emotional Prob Affectting Social Activity  1022
## 12 Female          Nervousness                                     1626
## 13 Female          Uncheerable                                     1425
## 14 Female          Calm                                            2527
## 15 Female          Downhearted                                     1975
## 16 Female          Happy                                           1283
```

PLot differences in male and female emotional states as adults 

```r
plot1 %>% 
  filter(em_state=="Nervousness" |em_state=="Uncheerable" | em_state=="Calm" | em_state=="Downhearted" | em_state=="Happy"  ) %>%
  ggplot(aes(x=em_state, y=count, group=Characteristics, fill=Characteristics))+
  geom_col(position="dodge")+
  coord_flip()
```

![](OG-Project_files/figure-html/unnamed-chunk-11-1.png)<!-- -->

Select Male and Female From characteristics

```r
plot2 <- data_subset %>% 
  filter(Characteristics=="Male" | Characteristics=="Female") %>% 
  pivot_longer(-Characteristics,
               names_to = "Soc_State",
               values_to = "Count")

plot2$Count <- as.numeric(plot2$Count)
plot2
```

```
## # A tibble: 16 x 3
##    Characteristics Soc_State                                      Count
##    <chr>           <chr>                                          <dbl>
##  1 Male            Activity Reduction                               610
##  2 Male            Less Accomplished                                903
##  3 Male            Phys_Emotional Prob Affectting Social Activity   796
##  4 Male            Nervousness                                     1328
##  5 Male            Uncheerable                                     1018
##  6 Male            Calm                                            2000
##  7 Male            Downhearted                                     1530
##  8 Male            Happy                                           1139
##  9 Female          Activity Reduction                               846
## 10 Female          Less Accomplished                               1155
## 11 Female          Phys_Emotional Prob Affectting Social Activity  1022
## 12 Female          Nervousness                                     1626
## 13 Female          Uncheerable                                     1425
## 14 Female          Calm                                            2527
## 15 Female          Downhearted                                     1975
## 16 Female          Happy                                           1283
```

PLot differences in male and female social and activity states as adults 

```r
plot2 %>% 
  filter(Soc_State=="Activity Reduction" |Soc_State=="Less Accomplished" | Soc_State=="Phys_Emotional Prob Affectting Social Activity" ) %>%
  ggplot(aes(x=Soc_State, y=Count, group=Characteristics, fill=Characteristics))+
  geom_col(position="dodge")+
  coord_flip()
```

![](OG-Project_files/figure-html/unnamed-chunk-13-1.png)<!-- -->
Filter cancer as characterisitic

```r
plot3 <- data_subset %>% 
  filter(Characteristics=="Leukemia" | Characteristics=="Hodgkin" | Characteristics=="NHL" | Characteristics=="CNS" | Characteristics=="Neuroblastoma" | Characteristics== "Non-Heritable Retinoblastoma" | Characteristics=="Heritable Retinoblastoma" |Characteristics=="Wilms" | Characteristics== "Bone Sarcoma" | Characteristics=="Soft Tissue Sarcoma" | Characteristics== "Other") %>% 
  rename(Diagnosis= "Characteristics")  %>% 
  select(Diagnosis, Nervousness, Uncheerable, Calm, Downhearted, Happy)  %>%
  pivot_longer(-Diagnosis,
               names_to = "Emotional_State",
               values_to = "Observations") %>%
  arrange(desc(Observations))

 
plot3$Observations <- as.numeric(plot3$Observations)
plot3
```

```
## # A tibble: 55 x 3
##    Diagnosis                    Emotional_State Observations
##    <chr>                        <chr>                  <dbl>
##  1 Neuroblastoma                Happy                     98
##  2 Leukemia                     Downhearted              977
##  3 Bone Sarcoma                 Uncheerable               96
##  4 Non-Heritable Retinoblastoma Happy                     94
##  5 CNS                          Downhearted              887
##  6 Heritable Retinoblastoma     Downhearted               88
##  7 Non-Heritable Retinoblastoma Uncheerable               86
##  8 Leukemia                     Nervousness              848
##  9 CNS                          Nervousness              771
## 10 Leukemia                     Uncheerable              686
## # … with 45 more rows
```

Graph

```r
plot3 %>% 
  ggplot(aes(x=Emotional_State, y=Observations, group=Diagnosis, fill=Diagnosis))+
  geom_col(position = "Dodge")+
  ggtitle("Cancer Vs Emotional State")
```

![](OG-Project_files/figure-html/unnamed-chunk-15-1.png)<!-- -->

Filter cancer and activity levels

```r
plot4 <- data_subset %>% 
  filter(Characteristics=="Leukemia" | Characteristics=="Hodgkin" | Characteristics=="NHL" | Characteristics=="CNS" | Characteristics=="Neuroblastoma" | Characteristics== "Non-Heritable Retinoblastoma" | Characteristics=="Heritable Retinoblastoma" |Characteristics=="Wilms" | Characteristics== "Bone Sarcoma" | Characteristics=="Soft Tissue Sarcoma" | Characteristics== "Other") %>% 
  rename(Diagnosis= "Characteristics")  %>% 
  select(Diagnosis, `Activity Reduction`, `Less Accomplished`, `Phys_Emotional Prob Affectting Social Activity`)  %>%
  pivot_longer(-Diagnosis,
               names_to = "Soc_State",
               values_to = "Observations") %>%
  arrange(desc(Observations))
 
plot4$Observations <- as.numeric(plot4$Observations)
plot4
```

```
## # A tibble: 33 x 3
##    Diagnosis                 Soc_State                              Observations
##    <chr>                     <chr>                                         <dbl>
##  1 Bone Sarcoma              Less Accomplished                                97
##  2 Hodgkin                   Activity Reduction                               93
##  3 Other                     Activity Reduction                               91
##  4 NHL                       Phys_Emotional Prob Affectting Social…           85
##  5 Neuroblastoma             Less Accomplished                                79
##  6 NHL                       Activity Reduction                               75
##  7 Bone Sarcoma              Activity Reduction                               75
##  8 Neuroblastoma             Phys_Emotional Prob Affectting Social…           72
##  9 Non-Heritable Retinoblas… Less Accomplished                                69
## 10 Heritable Retinoblastoma  Less Accomplished                                68
## # … with 23 more rows
```

Graph

```r
plot4 %>% 
  ggplot(aes(x=Soc_State, y=Observations, group=Diagnosis, fill=Diagnosis))+
  geom_col(position = "Dodge") +
  ggtitle("Cancer Vs Social State") +
  coord_flip() 
```

![](OG-Project_files/figure-html/unnamed-chunk-17-1.png)<!-- -->

Separate marriage status and social activities

```r
plot5 <- data_subset %>% 
  filter(Characteristics=="Single" | Characteristics=="Married" | Characteristics=="Separated" | Characteristics=="Divorced" | Characteristics=="Widowed") %>% 
  rename(Marriage_Status= "Characteristics")  %>% 
  select(Marriage_Status, `Activity Reduction`, `Less Accomplished`, `Phys_Emotional Prob Affectting Social Activity`)  %>%
  pivot_longer(-Marriage_Status,
               names_to = "Soc_State",
               values_to = "Observations") %>%
  arrange(desc(Observations))
 
plot5$Observations <- as.numeric(plot5$Observations)
plot5
```

```
## # A tibble: 15 x 3
##    Marriage_Status Soc_State                                      Observations
##    <chr>           <chr>                                                 <dbl>
##  1 Divorced        Activity Reduction                                       86
##  2 Widowed         Less Accomplished                                         8
##  3 Widowed         Phys_Emotional Prob Affectting Social Activity            8
##  4 Single          Activity Reduction                                      785
##  5 Widowed         Activity Reduction                                        6
##  6 Separated       Less Accomplished                                        50
##  7 Married         Less Accomplished                                       473
##  8 Married         Phys_Emotional Prob Affectting Social Activity          408
##  9 Separated       Phys_Emotional Prob Affectting Social Activity           36
## 10 Separated       Activity Reduction                                       35
## 11 Married         Activity Reduction                                      338
## 12 Divorced        Less Accomplished                                       118
## 13 Single          Less Accomplished                                      1125
## 14 Divorced        Phys_Emotional Prob Affectting Social Activity          104
## 15 Single          Phys_Emotional Prob Affectting Social Activity         1026
```

Graph

```r
plot5 %>% 
  ggplot(aes(x=Soc_State, y=Observations, group=Marriage_Status, fill=Marriage_Status))+
  geom_col(position = "Dodge") +
  ggtitle("Marriage Status Vs Social State") +
  coord_flip() 
```

![](OG-Project_files/figure-html/unnamed-chunk-19-1.png)<!-- -->

Select marriage status and emotional state

```r
plot6 <- data_subset %>% 
  filter(Characteristics=="Single" | Characteristics=="Married" | Characteristics=="Separated" | Characteristics=="Divorced" | Characteristics=="Widowed") %>% 
  rename(Marriage_Status= "Characteristics")  %>% 
  select(Marriage_Status, Nervousness, Uncheerable, Calm, Downhearted, Happy)  %>%
  pivot_longer(-Marriage_Status,
               names_to = "Emotional_State",
               values_to = "Observations") %>%
  arrange(desc(Observations))

 
plot6$Observations <- as.numeric(plot6$Observations)
plot6
```

```
## # A tibble: 25 x 3
##    Marriage_Status Emotional_State Observations
##    <chr>           <chr>                  <dbl>
##  1 Separated       Calm                      81
##  2 Married         Downhearted              792
##  3 Separated       Downhearted               79
##  4 Married         Nervousness              645
##  5 Married         Happy                    561
##  6 Separated       Nervousness               54
##  7 Separated       Uncheerable               51
##  8 Married         Uncheerable              500
##  9 Separated       Happy                     49
## 10 Single          Calm                    2437
## # … with 15 more rows
```

Graph

```r
plot6 %>% 
  ggplot(aes(x=Emotional_State, y=Observations, group=Marriage_Status, fill=Marriage_Status))+
  geom_col(position = "Dodge")+
  ggtitle("Marriage Status Vs Emotional State")
```

![](OG-Project_files/figure-html/unnamed-chunk-21-1.png)<!-- -->

Select ages and emotional state

```r
plot7 <- data_subset %>% 
  filter(Characteristics=="0-4 years" | Characteristics=="5-9 years" | Characteristics=="10-14 years") %>% 
  rename(Diagnosis_Age= "Characteristics")  %>% 
  select(Diagnosis_Age, Nervousness, Uncheerable, Calm, Downhearted, Happy)  %>%
  pivot_longer(-Diagnosis_Age,
               names_to = "Emotional_State",
               values_to = "Observations") %>%
  arrange(desc(Observations))

 
plot7$Observations <- as.numeric(plot7$Observations)
plot7
```

```
## # A tibble: 15 x 3
##    Diagnosis_Age Emotional_State Observations
##    <chr>         <chr>                  <dbl>
##  1 5-9 years     Downhearted              941
##  2 5-9 years     Nervousness              805
##  3 10-14 years   Nervousness              788
##  4 10-14 years   Happy                    752
##  5 10-14 years   Uncheerable              663
##  6 5-9 years     Happy                    646
##  7 5-9 years     Uncheerable              644
##  8 0-4 years     Calm                    1983
##  9 0-4 years     Downhearted             1555
## 10 0-4 years     Nervousness             1361
## 11 10-14 years   Calm                    1328
## 12 5-9 years     Calm                    1216
## 13 0-4 years     Uncheerable             1136
## 14 0-4 years     Happy                   1024
## 15 10-14 years   Downhearted             1009
```

Graph

```r
plot7 %>% 
  ggplot(aes(x=Emotional_State, y=Observations, group=Diagnosis_Age, fill=Diagnosis_Age))+
  geom_col(position = "Dodge")+
  ggtitle("Diagnosis Age Vs Emotional State")
```

![](OG-Project_files/figure-html/unnamed-chunk-23-1.png)<!-- -->


```r
plot8 <- data_subset %>% 
  filter(Characteristics=="0-4 years" | Characteristics=="5-9 years" | Characteristics=="10-14 years") %>% 
  rename(Diagnosis_Age= "Characteristics")  %>% 
  select(Diagnosis_Age, `Activity Reduction`, `Less Accomplished`, `Phys_Emotional Prob Affectting Social Activity`)  %>%
  pivot_longer(-Diagnosis_Age,
               names_to = "Soc_State",
               values_to = "Observations") %>%
  arrange(desc(Observations))
 
plot8$Observations <- as.numeric(plot8$Observations)
plot8
```

```
## # A tibble: 9 x 3
##   Diagnosis_Age Soc_State                                      Observations
##   <chr>         <chr>                                                 <dbl>
## 1 0-4 years     Less Accomplished                                       837
## 2 0-4 years     Phys_Emotional Prob Affectting Social Activity          762
## 3 10-14 years   Less Accomplished                                       643
## 4 0-4 years     Activity Reduction                                      595
## 5 5-9 years     Less Accomplished                                       578
## 6 10-14 years   Phys_Emotional Prob Affectting Social Activity          559
## 7 5-9 years     Phys_Emotional Prob Affectting Social Activity          497
## 8 10-14 years   Activity Reduction                                      458
## 9 5-9 years     Activity Reduction                                      403
```


```r
plot8 %>% 
  ggplot(aes(x=Soc_State, y=Observations, group=Diagnosis_Age, fill=Diagnosis_Age))+
  geom_col(position = "Dodge") +
  ggtitle("Diagnosis Age Vs Social State") +
  coord_flip() 
```

![](OG-Project_files/figure-html/unnamed-chunk-25-1.png)<!-- -->


