---
title: "Data Frames"
author: "Joel Ledford"
date: "Winter 2020"
output:
  html_document: 
    keep_md: yes
    theme: spacelab
    toc: yes
    toc_float: yes
  pdf_document:
    toc: yes
---

## Load tidyverse

```r
library("tidyverse")
```

```
## <U+2500><U+2500> Attaching packages <U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500> tidyverse 1.3.0 <U+2500><U+2500>
```

```
## <U+2713> ggplot2 3.2.1     <U+2713> purrr   0.3.3
## <U+2713> tibble  2.1.3     <U+2713> dplyr   0.8.3
## <U+2713> tidyr   1.0.0     <U+2713> stringr 1.4.0
## <U+2713> readr   1.3.1     <U+2713> forcats 0.4.0
```

```
## <U+2500><U+2500> Conflicts <U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500> tidyverse_conflicts() <U+2500><U+2500>
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

## Learning Goals
*At the end of this exercise, you will be able to:*    
1. Combine a series of vectors into a data frame.  
2. Name columns and rows in a data frame.  
3. Select columns and rows and use summary functions.   
4. Change data classes of columns in the data frame.  
5. Write your data frame to a csv file!  

## Data Frame
During the first part of lab, you learned how to work with vectors. Today we will organize the vectors into a new type of data structure called a **data frame**. The data frame is the most common way to organize data within R. You can think of a data frame as similar to an Excel spreadsheet. A data frame can store data of different types. 

Let's build three separate vectors of length (in), weight (oz), and sex of three ruby throated hummingbirds.

```r
Sex <- c("Male", "Female", "Male")
Length <- c(3.2, 3.7, 3.4)
Weight <- c(2.9, 4.0, 3.1)
```

Here we combine our three vectors to create a data frame with the function `data.frame()`.

```r
hbirds <- data.frame(Sex, Length, Weight)
hbirds
```

```
##      Sex Length Weight
## 1   Male    3.2    2.9
## 2 Female    3.7    4.0
## 3   Male    3.4    3.1
```

Notice that not only are the data neat and clean looking, there is also information provided about the type of data in the frame. `dbl` means that the value is a type of numeric [double precision floating point](http://uc-r.github.io/integer_double/). 

What are the column names of our data frame? Notice that R defaulted to using the names of our vectors, but we could name them something else when creating the data frame, or rename them later.

```r
names(hbirds)
```

```
## [1] "Sex"    "Length" "Weight"
```

Let's use lowercase names when we create the data frame. We just changed to lowercase here, but we could use any names we wish.

```r
hbirds <- data.frame(sex = Sex,length_in = Length, weight_oz = Weight)
names(hbirds)
```

```
## [1] "sex"       "length_in" "weight_oz"
```


```r
hbirds
```

```
##      sex length_in weight_oz
## 1   Male       3.2       2.9
## 2 Female       3.7       4.0
## 3   Male       3.4       3.1
```

## Accessing Data Frame Columns and Rows 
The same methods of selecting elements in a vector apply to data frames. We use `[]`. But now we have two positions where the first applies to the rows, and the second to the columns.  

The first row.  

```r
hbirds[1,]
```

```
##    sex length_in weight_oz
## 1 Male       3.2       2.9
```

The third column.  

```r
hbirds[,3]
```

```
## [1] 2.9 4.0 3.1
```

We can also select values in an entire column using the `$` sign. This can be useful for calculations. Here we calculate the mean of all of the birds weights. 

```r
w <- hbirds$weight_oz
mean(w)
```

```
## [1] 3.333333
```

## Summaries
We can also summarize our entire data frame with the`summary()` function.

```r
summary(hbirds)
```

```
##      sex      length_in       weight_oz    
##  Female:1   Min.   :3.200   Min.   :2.900  
##  Male  :2   1st Qu.:3.300   1st Qu.:3.000  
##             Median :3.400   Median :3.100  
##             Mean   :3.433   Mean   :3.333  
##             3rd Qu.:3.550   3rd Qu.:3.550  
##             Max.   :3.700   Max.   :4.000
```

## Glimpse
`glimpse()` is another useful summary function.

```r
glimpse(hbirds)
```

```
## Observations: 3
## Variables: 3
## $ sex       <fct> Male, Female, Male
## $ length_in <dbl> 3.2, 3.7, 3.4
## $ weight_oz <dbl> 2.9, 4.0, 3.1
```

```r
anyNA(hbirds)
```

```
## [1] FALSE
```
## Adding Rows
We can add a new bird's data with the `rbind()` function, known as row bind. It will bind our new vector to our data frame row-wise.

```r
new_bird <- c("Female", 3.6, 3.9)
new_bird
```

```
## [1] "Female" "3.6"    "3.9"
```


```r
hbirds<- rbind(hbirds, new_bird)
hbirds
```

```
##      sex length_in weight_oz
## 1   Male       3.2       2.9
## 2 Female       3.7         4
## 3   Male       3.4       3.1
## 4 Female       3.6       3.9
```

```r
height <- c(2, 2.3, 4, .9)
```

```r
hbirds <- cbind(hbirds, height)
hbirds
```

```
##      sex length_in weight_oz height
## 1   Male       3.2       2.9    2.0
## 2 Female       3.7         4    2.3
## 3   Male       3.4       3.1    4.0
## 4 Female       3.6       3.9    0.9
```
## Adding Columns
What if we come across more data and we want to add it to our data frame? We can do that with the `$` operator.

```r
hbirds$neighborhood <- c("Lakewood", "Brentwood", "Lakewood", "Scenic Heights")
hbirds
```

```
##      sex length_in weight_oz height   neighborhood
## 1   Male       3.2       2.9    2.0       Lakewood
## 2 Female       3.7         4    2.3      Brentwood
## 3   Male       3.4       3.1    4.0       Lakewood
## 4 Female       3.6       3.9    0.9 Scenic Heights
```

## Changing Column Classes
Great, we added our new column, but it's a character and not a factor. A factor is a special type of character vector with predefined levels. 

```r
class(hbirds$neighborhood)
```

```
## [1] "character"
```

```r
hbirds$neighborhood <- as.factor(hbirds$neighborhood)
```


```r
class(hbirds$neighborhood)
```

```
## [1] "factor"
```

`levels()` will give you a list of the different levels within a factor.  

```r
levels(hbirds$neighborhood)
```

```
## [1] "Brentwood"      "Lakewood"       "Scenic Heights"
```

```r
levels(hbirds$sex)
```

```
## [1] "Female" "Male"
```

## Writing Data to File
We should save our hbirds data frame so we can use it again later! There are many ways to save data in R, here we write our data frame to a csv file. We use  `row.names = FALSE` to avoid row numbers from printing out. 

```r
write.csv(hbirds, "hbirds_data.csv", row.names = FALSE)
```

## Practice
Below are data collected by three scientists (Jill, Steve, Susan in order) measuring temperatures of three hot springs near Mono Lake.

```r
temp <- c(36.25, 35.40, 35.30, 35.15, 35.35, 33.35, 30.70, 29.65, 29.20)
name <- c("Jill","Susan", "Steve", "Jill","Susan", "Steve", "Jill","Susan", "Steve")
spring <- c("Buckeye", "Buckeye", "Buckeye", "Benton", "Benton", "Benton", "Travertine", "Travertine", "Travertine")
```

1. Build a data frame called `hsprings` with the above data. Name the temperature column `temp_C`. Print out the data frame.  

```r
hsprings <- data.frame(temp, name, spring)
hsprings
```

```
##    temp  name     spring
## 1 36.25  Jill    Buckeye
## 2 35.40 Susan    Buckeye
## 3 35.30 Steve    Buckeye
## 4 35.15  Jill     Benton
## 5 35.35 Susan     Benton
## 6 33.35 Steve     Benton
## 7 30.70  Jill Travertine
## 8 29.65 Susan Travertine
## 9 29.20 Steve Travertine
```
2. Change the column titled `name` to `scientist`, leave the other column names the same. Print out the data frame names.  

```r
hsprings <- data.frame(temp=temp,scientists=name, spring=spring)
names(hsprings)
```

```
## [1] "temp"       "scientists" "spring"
```

```r
hsprings
```

```
##    temp scientists     spring
## 1 36.25       Jill    Buckeye
## 2 35.40      Susan    Buckeye
## 3 35.30      Steve    Buckeye
## 4 35.15       Jill     Benton
## 5 35.35      Susan     Benton
## 6 33.35      Steve     Benton
## 7 30.70       Jill Travertine
## 8 29.65      Susan Travertine
## 9 29.20      Steve Travertine
```
3. Our scientists forgot to record the depth data for each spring. Here it is as a vector, add it as a new column called depth_ft: `c(4.15, 4.13, 4.12, 3.21, 3.23, 3.20, 5.67, 5.65, 5.66)`. Print out the data frame.

```r
depth_ft <- c(4.15, 4.13, 4.12, 3.21, 3.23, 3.20, 5.67, 5.65, 5.66)
```

```r
hsprings <- cbind(hsprings, depth_ft)
hsprings
```

```
##    temp scientists     spring depth_ft
## 1 36.25       Jill    Buckeye     4.15
## 2 35.40      Susan    Buckeye     4.13
## 3 35.30      Steve    Buckeye     4.12
## 4 35.15       Jill     Benton     3.21
## 5 35.35      Susan     Benton     3.23
## 6 33.35      Steve     Benton     3.20
## 7 30.70       Jill Travertine     5.67
## 8 29.65      Susan Travertine     5.65
## 9 29.20      Steve Travertine     5.66
```
4. Calculate the mean temperature of all of the temperature measurements.

```r
t <- hsprings$temp
mean(t)
```

```
## [1] 33.37222
```

5. What is the class of the scientist column? Use the `levels()` command to see all the unique levels.  

```r
class(hsprings$scientists)
```

```
## [1] "factor"
```

```r
levels(hsprings$scientists)
```

```
## [1] "Jill"  "Steve" "Susan"
```

6. Save your hot springs data as a csv file! Do not allow row names. 

```r
write.csv(hsprings, "hsprings_data.csv", row.names = FALSE)
```

## Wrap-up
Please review the learning goals and be sure to use the code here as a reference when completing the homework.  

-->[Home](https://jmledford3115.github.io/datascibiol/)
