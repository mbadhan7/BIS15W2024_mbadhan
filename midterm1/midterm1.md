---
title: "Midterm 1 W24"
author: "Mohit Badhan"
date: "2024-02-06"
output:
  html_document: 
    keep_md: yes
  pdf_document: default
---

## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your code must be organized, clean, and run free from errors. Remember, you must remove the `#` for any included code chunks to run. Be sure to add your name to the author header above. 

Your code must knit in order to be considered. If you are stuck and cannot answer a question, then comment out your code and knit the document. You may use your notes, labs, and homework to help you complete this exam. Do not use any other resources- including AI assistance.  

Don't forget to answer any questions that are asked in the prompt!  

Be sure to push your completed midterm to your repository. This exam is worth 30 points.  

## Background
In the data folder, you will find data related to a study on wolf mortality collected by the National Park Service. You should start by reading the `README_NPSwolfdata.pdf` file. This will provide an abstract of the study and an explanation of variables.  

The data are from: Cassidy, Kira et al. (2022). Gray wolf packs and human-caused wolf mortality. [Dryad](https://doi.org/10.5061/dryad.mkkwh713f). 

## Load the libraries

```r
library("tidyverse")
library("janitor")
```

## Load the wolves data
In these data, the authors used `NULL` to represent missing values. I am correcting this for you below and using `janitor` to clean the column names.

```r
wolves <- read.csv("data/NPS_wolfmortalitydata.csv", na = c("NULL")) %>% clean_names()
```

## Questions
Problem 1. (1 point) Let's start with some data exploration. What are the variable (column) names?  

The variable (column) names are park, biolyr, pack, packcode, packsizeAug, mortYN, mortALL, mortLEAD, mortNONLEAD, reprody1, and persisty.

Problem 2. (1 point) Use the function of your choice to summarize the data and get an idea of its structure.  


```r
summary(wolves)
```

```
##      park               biolyr         pack              packcode     
##  Length:864         Min.   :1986   Length:864         Min.   :  2.00  
##  Class :character   1st Qu.:1999   Class :character   1st Qu.: 48.00  
##  Mode  :character   Median :2006   Mode  :character   Median : 86.50  
##                     Mean   :2005                      Mean   : 91.39  
##                     3rd Qu.:2012                      3rd Qu.:133.00  
##                     Max.   :2021                      Max.   :193.00  
##                                                                       
##   packsize_aug       mort_yn          mort_all         mort_lead      
##  Min.   : 0.000   Min.   :0.0000   Min.   : 0.0000   Min.   :0.00000  
##  1st Qu.: 5.000   1st Qu.:0.0000   1st Qu.: 0.0000   1st Qu.:0.00000  
##  Median : 8.000   Median :0.0000   Median : 0.0000   Median :0.00000  
##  Mean   : 8.789   Mean   :0.1956   Mean   : 0.3715   Mean   :0.09552  
##  3rd Qu.:12.000   3rd Qu.:0.0000   3rd Qu.: 0.0000   3rd Qu.:0.00000  
##  Max.   :37.000   Max.   :1.0000   Max.   :24.0000   Max.   :3.00000  
##  NA's   :55                                          NA's   :16       
##   mort_nonlead        reprody1        persisty1     
##  Min.   : 0.0000   Min.   :0.0000   Min.   :0.0000  
##  1st Qu.: 0.0000   1st Qu.:1.0000   1st Qu.:1.0000  
##  Median : 0.0000   Median :1.0000   Median :1.0000  
##  Mean   : 0.2641   Mean   :0.7629   Mean   :0.8865  
##  3rd Qu.: 0.0000   3rd Qu.:1.0000   3rd Qu.:1.0000  
##  Max.   :22.0000   Max.   :1.0000   Max.   :1.0000  
##  NA's   :12        NA's   :71       NA's   :9
```


Problem 3. (3 points) Which parks/ reserves are represented in the data? Don't just use the abstract, pull this information from the data.  


```r
table(wolves$park)
```

```
## 
## DENA GNTP  VNP  YNP YUCH 
##  340   77   48  248  151
```


Problem 4. (4 points) Which park has the largest number of wolf packs?


```r
wolves %>%
  group_by(park) %>%
  summarize(large_pack=sum(packsize_aug, na.rm=T), n=n()) %>%
  arrange(desc(large_pack))
```

```
## # A tibble: 5 × 3
##   park  large_pack     n
##   <chr>      <dbl> <int>
## 1 YNP        2731    248
## 2 DENA       2500    340
## 3 YUCH       1048    151
## 4 GNTP        781.    77
## 5 VNP          50     48
```
YNP has the largest number of wolf packs.


Problem 5. (4 points) Which park has the highest total number of human-caused mortalities `mort_all`?


```r
wolves %>%
  group_by(park) %>%
  summarize(mort_new=sum(mort_all, na.rm=T), n=n()) %>%
  arrange(desc(mort_new))
```

```
## # A tibble: 5 × 3
##   park  mort_new     n
##   <chr>    <int> <int>
## 1 YUCH       136   151
## 2 YNP         72   248
## 3 DENA        64   340
## 4 GNTP        38    77
## 5 VNP         11    48
```
YUCH has the highest total number of human-caused mortalities.


The wolves in [Yellowstone National Park](https://www.nps.gov/yell/learn/nature/wolf-restoration.htm) are an incredible conservation success story. Let's focus our attention on this park.  

Problem 6. (2 points) Create a new object "ynp" that only includes the data from Yellowstone National Park.  


```r
ynp <- wolves %>%
  filter(park == "YNP")
```


Problem 7. (3 points) Among the Yellowstone wolf packs, the [Druid Peak Pack](https://www.pbs.org/wnet/nature/in-the-valley-of-the-wolves-the-druid-wolf-pack-story/209/) is one of most famous. What was the average pack size of this pack for the years represented in the data?


```r
ynp %>%
  filter(pack=="druid") %>%
  summarize(mean_ps=mean(packsize_aug, na.rm=T))
```

```
##    mean_ps
## 1 13.93333
```
The avergae pack size of this pack for years represented in the data was 13.93.

Problem 8. (4 points) Pack dynamics can be hard to predict- even for strong packs like the Druid Peak pack. At which year did the Druid Peak pack have the largest pack size? What do you think happened in 2010?


```r
wolves %>%
  filter(pack == "druid") %>%
  group_by(biolyr) %>%
  summarize(large_druid=sum(packsize_aug, na.rm=T), n=n()) %>%
  arrange(desc(large_druid))
```

```
## # A tibble: 15 × 3
##    biolyr large_druid     n
##     <int>       <dbl> <int>
##  1   2001          37     1
##  2   2000          27     1
##  3   2008          21     1
##  4   2003          18     1
##  5   2007          18     1
##  6   2002          16     1
##  7   2006          15     1
##  8   2004          13     1
##  9   2009          12     1
## 10   1999           9     1
## 11   1998           8     1
## 12   1996           5     1
## 13   1997           5     1
## 14   2005           5     1
## 15   2010           0     1
```
In 2001, the Druid Peak pack had the largest packsize. In 2010, the Druid Peak pack could have been hunted and their own pack population size may have had competition within it in which their packsize resulted in 0 for the fall of 2010.


Problem 9. (5 points) Among the YNP wolf packs, which one has had the highest overall persistence `persisty1` for the years represented in the data? Look this pack up online and tell me what is unique about its behavior- specifically, what prey animals does this pack specialize on?  


```r
ynp %>%
  group_by(pack) %>%
  summarize(max_pers=sum(persisty1, na.rm=T)) %>%
  arrange(desc(max_pers))
```

```
## # A tibble: 46 × 2
##    pack        max_pers
##    <chr>          <int>
##  1 mollies           26
##  2 cougar            20
##  3 yelldelta         18
##  4 druid             13
##  5 leopold           12
##  6 agate             10
##  7 8mile              9
##  8 canyon             9
##  9 gibbon/mary        9
## 10 nezperce           9
## # ℹ 36 more rows
```
The mollies pack had the highest overall persistence in the YNP wolf packs. Their unique behavior is that they are well-known for killing large animals such as bison and have regular interations with bears.

https://www.yellowstonewolf.org/yellowstones_wolves.php?pack_id=6

Problem 10. (3 points) Perform one analysis or exploration of your choice on the `wolves` data. Your answer needs to include at least two lines of code and not be a summary function.  


```r
wolves %>%
  group_by(park, pack, biolyr, mort_all) %>%
  summarize(mean_pers=mean(packsize_aug, na.rm=T)) %>%
  arrange(desc(mean_pers))
```

```
## `summarise()` has grouped output by 'park', 'pack', 'biolyr'. You can override
## using the `.groups` argument.
```

```
## # A tibble: 864 × 5
## # Groups:   park, pack, biolyr [864]
##    park  pack        biolyr mort_all mean_pers
##    <chr> <chr>        <int>    <int>     <dbl>
##  1 YNP   druid         2001        0      37  
##  2 YNP   junction      2020        0      35  
##  3 DENA  East Fork     1990        0      33  
##  4 YNP   leopold       2004        0      28  
##  5 DENA  East Fork     1989        0      27  
##  6 YNP   8mile         2014        1      27  
##  7 YNP   druid         2000        1      27  
##  8 GNTP  Buffalo       2009        1      26.4
##  9 YNP   gibbon/mary   2009        1      26  
## 10 YNP   leopold       2005        0      26  
## # ℹ 854 more rows
```




