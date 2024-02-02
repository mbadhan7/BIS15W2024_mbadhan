---
title: "Lab 7 Homework"
author: "Mohit Badhan"
date: "2024-02-01"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the libraries

```r
library(tidyverse)
library(janitor)
library(skimr)
```

For this assignment we are going to work with a large data set from the [United Nations Food and Agriculture Organization](http://www.fao.org/about/en/) on world fisheries. These data are pretty wild, so we need to do some cleaning. First, load the data.  

Load the data `FAO_1950to2012_111914.csv` as a new object titled `fisheries`.

```r
fisheries <- readr::read_csv(file = "data/FAO_1950to2012_111914.csv")
```

```
## Rows: 17692 Columns: 71
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (69): Country, Common name, ISSCAAP taxonomic group, ASFIS species#, ASF...
## dbl  (2): ISSCAAP group#, FAO major fishing area
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

1. Do an exploratory analysis of the data (your choice). What are the names of the variables, what are the dimensions, are there any NA's, what are the classes of the variables?  

```r
skim(fisheries)
```

```
## Warning: There was 1 warning in `dplyr::summarize()`.
## ℹ In argument: `dplyr::across(tidyselect::any_of(variable_names),
##   mangled_skimmers$funs)`.
## ℹ In group 0: .
## Caused by warning:
## ! There were 119 warnings in `dplyr::summarize()`.
## The first warning was:
## ℹ In argument: `dplyr::across(tidyselect::any_of(variable_names),
##   mangled_skimmers$funs)`.
## Caused by warning in `grepl()`:
## ! unable to translate 'Cura<e7>ao' to a wide string
## ℹ Run `dplyr::last_dplyr_warnings()` to see the 118 remaining warnings.
```


Table: Data summary

|                         |          |
|:------------------------|:---------|
|Name                     |fisheries |
|Number of rows           |17692     |
|Number of columns        |71        |
|_______________________  |          |
|Column type frequency:   |          |
|character                |69        |
|numeric                  |2         |
|________________________ |          |
|Group variables          |None      |


**Variable type: character**

|skim_variable           | n_missing| complete_rate| min| max| empty| n_unique| whitespace|
|:-----------------------|---------:|-------------:|---:|---:|-----:|--------:|----------:|
|Country                 |         0|          1.00|   4|  25|     0|      204|          0|
|Common name             |         0|          1.00|   3|  30|     0|     1553|          0|
|ISSCAAP taxonomic group |         0|          1.00|   5|  36|     0|       30|          0|
|ASFIS species#          |         0|          1.00|  10|  13|     0|     1553|          0|
|ASFIS species name      |         0|          1.00|   6|  32|     0|     1548|          0|
|Measure                 |         0|          1.00|  17|  17|     0|        1|          0|
|1950                    |     15561|          0.12|   1|   6|     0|      513|          0|
|1951                    |     15550|          0.12|   1|   7|     0|      536|          0|
|1952                    |     15501|          0.12|   1|   7|     0|      553|          0|
|1953                    |     15439|          0.13|   1|   6|     0|      570|          0|
|1954                    |     15417|          0.13|   1|   7|     0|      588|          0|
|1955                    |     15382|          0.13|   1|   7|     0|      589|          0|
|1956                    |     15331|          0.13|   1|   7|     0|      633|          0|
|1957                    |     15253|          0.14|   1|   7|     0|      627|          0|
|1958                    |     15138|          0.14|   1|   6|     0|      643|          0|
|1959                    |     15110|          0.15|   1|   7|     0|      641|          0|
|1960                    |     15016|          0.15|   1|   7|     0|      673|          0|
|1961                    |     14922|          0.16|   1|   8|     0|      713|          0|
|1962                    |     14801|          0.16|   1|   8|     0|      729|          0|
|1963                    |     14707|          0.17|   1|   8|     0|      760|          0|
|1964                    |     14349|          0.19|   1|   8|     0|      759|          0|
|1965                    |     14241|          0.20|   1|   8|     0|      798|          0|
|1966                    |     14187|          0.20|   1|   8|     0|      801|          0|
|1967                    |     14047|          0.21|   1|   8|     0|      815|          0|
|1968                    |     13963|          0.21|   1|   8|     0|      829|          0|
|1969                    |     13920|          0.21|   1|   8|     0|      853|          0|
|1970                    |     13113|          0.26|   1|   8|     0|     1225|          0|
|1971                    |     12925|          0.27|   1|   8|     0|     1326|          0|
|1972                    |     12749|          0.28|   1|   8|     0|     1372|          0|
|1973                    |     12673|          0.28|   1|   8|     0|     1432|          0|
|1974                    |     12583|          0.29|   1|   8|     0|     2601|          0|
|1975                    |     12333|          0.30|   1|   8|     0|     2767|          0|
|1976                    |     12177|          0.31|   1|   8|     0|     2804|          0|
|1977                    |     12014|          0.32|   1|   8|     0|     2867|          0|
|1978                    |     11847|          0.33|   1|   8|     0|     2901|          0|
|1979                    |     11820|          0.33|   1|   8|     0|     2932|          0|
|1980                    |     11747|          0.34|   1|   8|     0|     2956|          0|
|1981                    |     11713|          0.34|   1|   8|     0|     2996|          0|
|1982                    |     11558|          0.35|   1|   9|     0|     3030|          0|
|1983                    |     11453|          0.35|   1|   8|     0|     3031|          0|
|1984                    |     11309|          0.36|   1|   8|     0|     3076|          0|
|1985                    |     11212|          0.37|   1|   8|     0|     3161|          0|
|1986                    |     11086|          0.37|   1|   8|     0|     3242|          0|
|1987                    |     10930|          0.38|   1|   8|     0|     3255|          0|
|1988                    |     10493|          0.41|   1|   8|     0|     3435|          0|
|1989                    |     10435|          0.41|   1|   8|     0|     3425|          0|
|1990                    |     10293|          0.42|   1|   8|     0|     3446|          0|
|1991                    |     10364|          0.41|   1|   8|     0|     3420|          0|
|1992                    |     10435|          0.41|   1|   8|     0|     3322|          0|
|1993                    |     10522|          0.41|   1|   8|     0|     3313|          0|
|1994                    |     10400|          0.41|   1|   8|     0|     3313|          0|
|1995                    |     10148|          0.43|   1|   8|     0|     3329|          0|
|1996                    |      9990|          0.44|   1|   7|     0|     3358|          0|
|1997                    |      9773|          0.45|   1|   9|     0|     3393|          0|
|1998                    |      9579|          0.46|   1|   9|     0|     3399|          0|
|1999                    |      9265|          0.48|   1|   9|     0|     3428|          0|
|2000                    |      8899|          0.50|   1|   9|     0|     3481|          0|
|2001                    |      8646|          0.51|   1|   9|     0|     3490|          0|
|2002                    |      8590|          0.51|   1|   9|     0|     3507|          0|
|2003                    |      8383|          0.53|   1|   9|     0|     3482|          0|
|2004                    |      7977|          0.55|   1|   9|     0|     3505|          0|
|2005                    |      7822|          0.56|   1|   9|     0|     3532|          0|
|2006                    |      7699|          0.56|   1|   9|     0|     3565|          0|
|2007                    |      7589|          0.57|   1|   8|     0|     3551|          0|
|2008                    |      7667|          0.57|   1|   8|     0|     3537|          0|
|2009                    |      7573|          0.57|   1|   8|     0|     3572|          0|
|2010                    |      7499|          0.58|   1|   8|     0|     3590|          0|
|2011                    |      7371|          0.58|   1|   8|     0|     3618|          0|
|2012                    |      7336|          0.59|   1|   8|     0|     3609|          0|


**Variable type: numeric**

|skim_variable          | n_missing| complete_rate|  mean|    sd| p0| p25| p50| p75| p100|hist  |
|:----------------------|---------:|-------------:|-----:|-----:|--:|---:|---:|---:|----:|:-----|
|ISSCAAP group#         |         0|             1| 37.38|  7.88| 11|  33|  36|  38|   77|▁▇▂▁▁ |
|FAO major fishing area |         0|             1| 45.34| 18.33| 18|  31|  37|  57|   88|▇▇▆▃▃ |

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


2. Use `janitor` to rename the columns and make them easier to use. As part of this cleaning step, change `country`, `isscaap_group_number`, `asfis_species_number`, and `fao_major_fishing_area` to data class factor. 

```r
data_class_factor <- clean_names(fisheries)
```


```r
colnames(data_class_factor)
```

```
##  [1] "country"                 "common_name"            
##  [3] "isscaap_group_number"    "isscaap_taxonomic_group"
##  [5] "asfis_species_number"    "asfis_species_name"     
##  [7] "fao_major_fishing_area"  "measure"                
##  [9] "x1950"                   "x1951"                  
## [11] "x1952"                   "x1953"                  
## [13] "x1954"                   "x1955"                  
## [15] "x1956"                   "x1957"                  
## [17] "x1958"                   "x1959"                  
## [19] "x1960"                   "x1961"                  
## [21] "x1962"                   "x1963"                  
## [23] "x1964"                   "x1965"                  
## [25] "x1966"                   "x1967"                  
## [27] "x1968"                   "x1969"                  
## [29] "x1970"                   "x1971"                  
## [31] "x1972"                   "x1973"                  
## [33] "x1974"                   "x1975"                  
## [35] "x1976"                   "x1977"                  
## [37] "x1978"                   "x1979"                  
## [39] "x1980"                   "x1981"                  
## [41] "x1982"                   "x1983"                  
## [43] "x1984"                   "x1985"                  
## [45] "x1986"                   "x1987"                  
## [47] "x1988"                   "x1989"                  
## [49] "x1990"                   "x1991"                  
## [51] "x1992"                   "x1993"                  
## [53] "x1994"                   "x1995"                  
## [55] "x1996"                   "x1997"                  
## [57] "x1998"                   "x1999"                  
## [59] "x2000"                   "x2001"                  
## [61] "x2002"                   "x2003"                  
## [63] "x2004"                   "x2005"                  
## [65] "x2006"                   "x2007"                  
## [67] "x2008"                   "x2009"                  
## [69] "x2010"                   "x2011"                  
## [71] "x2012"
```


We need to deal with the years because they are being treated as characters and start with an X. We also have the problem that the column names that are years actually represent data. We haven't discussed tidy data yet, so here is some help. You should run this ugly chunk to transform the data for the rest of the homework. It will only work if you have used janitor to rename the variables in question 2!  

```r
fisheries_tidy <- data_class_factor %>% 
  pivot_longer(-c(country,common_name,isscaap_group_number,isscaap_taxonomic_group,asfis_species_number,asfis_species_name,fao_major_fishing_area,measure),
               names_to = "year",
               values_to = "catch",
               values_drop_na = TRUE) %>% 
  mutate(year= as.numeric(str_replace(year, 'x', ''))) %>% 
  mutate(catch= str_replace(catch, c(' F'), replacement = '')) %>% 
  mutate(catch= str_replace(catch, c('...'), replacement = '')) %>% 
  mutate(catch= str_replace(catch, c('-'), replacement = '')) %>% 
  mutate(catch= str_replace(catch, c('0 0'), replacement = ''))

fisheries_tidy$catch <- as.numeric(fisheries_tidy$catch)
```

3. How many countries are represented in the data? Provide a count and list their names.

```r
fisheries_tidy %>%
  tabyl(country)
```

```
##                    country     n      percent
##                    Albania   934 2.478959e-03
##                    Algeria  1561 4.143100e-03
##             American Samoa   556 1.475697e-03
##                     Angola  2119 5.624106e-03
##                   Anguilla   129 3.423830e-04
##        Antigua and Barbuda   356 9.448710e-04
##                  Argentina  3403 9.032011e-03
##                      Aruba   172 4.565107e-04
##                  Australia  8183 2.171876e-02
##                    Bahamas   423 1.122698e-03
##                    Bahrain  1169 3.102680e-03
##                 Bangladesh   169 4.485483e-04
##                   Barbados   795 2.110035e-03
##                    Belgium  2530 6.714954e-03
##                     Belize  1075 2.853192e-03
##                      Benin  1419 3.766213e-03
##                    Bermuda   846 2.245396e-03
##   Bonaire/S.Eustatius/Saba     4 1.061653e-05
##     Bosnia and Herzegovina    21 5.573677e-05
##                     Brazil  4784 1.269737e-02
##   British Indian Ocean Ter    97 2.574508e-04
##     British Virgin Islands   332 8.811719e-04
##          Brunei Darussalam   186 4.936686e-04
##                   Bulgaria  1596 4.235995e-03
##                 Cabo Verde   462 1.226209e-03
##                   Cambodia   238 6.316834e-04
##                   Cameroon  1340 3.556537e-03
##                     Canada  5099 1.353342e-02
##             Cayman Islands    84 2.229471e-04
##            Channel Islands  1313 3.484875e-03
##                      Chile  3878 1.029272e-02
##                      China  2801 7.434224e-03
##       China, Hong Kong SAR  1782 4.729663e-03
##           China, Macao SAR   206 5.467512e-04
##                   Colombia  2710 7.192698e-03
##                    Comoros   965 2.561237e-03
##    Congo, Dem. Rep. of the   484 1.284600e-03
##         Congo, Republic of  1527 4.052860e-03
##               Cook Islands   810 2.149847e-03
##                 Costa Rica  1171 3.107989e-03
##                    Croatia   947 2.513463e-03
##                       Cuba  2981 7.911968e-03
##                 Cura\xe7ao    18 4.777438e-05
##                     Cyprus  1703 4.519987e-03
##           C\xf4te d'Ivoire  1859 4.934032e-03
##                    Denmark  3741 9.929108e-03
##                   Djibouti   352 9.342545e-04
##                   Dominica   213 5.653301e-04
##         Dominican Republic  1958 5.196791e-03
##                    Ecuador  1595 4.233341e-03
##                      Egypt  2467 6.547744e-03
##                El Salvador   620 1.645562e-03
##          Equatorial Guinea   551 1.462427e-03
##                    Eritrea   653 1.733148e-03
##                    Estonia  1088 2.887696e-03
##                   Ethiopia   129 3.423830e-04
##     Falkland Is.(Malvinas)   502 1.332374e-03
##              Faroe Islands  2283 6.059384e-03
##          Fiji, Republic of  1798 4.772129e-03
##                    Finland   706 1.873817e-03
##                     France 10639 2.823731e-02
##              French Guiana   231 6.131045e-04
##           French Polynesia   672 1.783577e-03
##       French Southern Terr   139 3.689244e-04
##                      Gabon  1089 2.890350e-03
##                     Gambia  1214 3.222116e-03
##                    Georgia   428 1.135969e-03
##                    Germany  4813 1.277434e-02
##                      Ghana  2462 6.534473e-03
##                  Gibraltar    61 1.619021e-04
##                     Greece  4091 1.085805e-02
##                  Greenland  1311 3.479567e-03
##                    Grenada  1635 4.339506e-03
##                 Guadeloupe   372 9.873371e-04
##                       Guam   520 1.380149e-03
##                  Guatemala   622 1.650870e-03
##                     Guinea   697 1.849930e-03
##               GuineaBissau   634 1.682720e-03
##                     Guyana   251 6.661872e-04
##                      Haiti   204 5.414429e-04
##                   Honduras   842 2.234779e-03
##                    Iceland  2346 6.226594e-03
##                      India  5588 1.483129e-02
##                  Indonesia  9274 2.461442e-02
##     Iran (Islamic Rep. of)  1210 3.211500e-03
##                       Iraq   150 3.981198e-04
##                    Ireland  3235 8.586117e-03
##                Isle of Man   952 2.526734e-03
##                     Israel  1359 3.606966e-03
##                      Italy  4567 1.212142e-02
##                    Jamaica   149 3.954657e-04
##                      Japan 15429 4.095060e-02
##                     Jordan   226 5.998339e-04
##                      Kenya   958 2.542659e-03
##                   Kiribati   875 2.322366e-03
##   Korea, Dem. People's Rep   210 5.573677e-04
##         Korea, Republic of 10824 2.872833e-02
##                     Kuwait   805 2.136576e-03
##                     Latvia  1101 2.922199e-03
##                    Lebanon   614 1.629637e-03
##                    Liberia  1514 4.018356e-03
##                      Libya   578 1.534088e-03
##                  Lithuania  1274 3.381364e-03
##                 Madagascar  1008 2.675365e-03
##                   Malaysia  6963 1.848072e-02
##                   Maldives   487 1.292562e-03
##                      Malta  2156 5.722309e-03
##           Marshall Islands   292 7.750066e-04
##                 Martinique   672 1.783577e-03
##                 Mauritania  1501 3.983852e-03
##                  Mauritius   991 2.630245e-03
##                    Mayotte   194 5.149016e-04
##                     Mexico  6202 1.646093e-02
##  Micronesia, Fed.States of   413 1.096157e-03
##                     Monaco    43 1.141277e-04
##                 Montenegro   168 4.458942e-04
##                 Montserrat    63 1.672103e-04
##                    Morocco  4758 1.262836e-02
##                 Mozambique   434 1.151893e-03
##                    Myanmar   117 3.105335e-04
##                    Namibia   905 2.401990e-03
##                      Nauru   150 3.981198e-04
##                Netherlands  2944 7.813765e-03
##       Netherlands Antilles   338 8.970966e-04
##              New Caledonia   789 2.094110e-03
##                New Zealand  4594 1.219308e-02
##                  Nicaragua   904 2.399335e-03
##                    Nigeria  1479 3.925461e-03
##                       Niue   145 3.848492e-04
##             Norfolk Island    41 1.088194e-04
##       Northern Mariana Is.   488 1.295216e-03
##                     Norway  3747 9.945033e-03
##                       Oman  1086 2.882387e-03
##                  Other nei  1556 4.129830e-03
##                   Pakistan  2166 5.748850e-03
##                      Palau   636 1.688028e-03
##    Palestine, Occupied Tr.   429 1.138623e-03
##                     Panama  1773 4.705776e-03
##           Papua New Guinea   686 1.820735e-03
##                       Peru  2767 7.343983e-03
##                Philippines  4548 1.207099e-02
##           Pitcairn Islands    63 1.672103e-04
##                     Poland  2553 6.775999e-03
##                   Portugal 11570 3.070831e-02
##                Puerto Rico   918 2.436493e-03
##                      Qatar   941 2.497538e-03
##                    Romania  1738 4.612882e-03
##         Russian Federation  4736 1.256997e-02
##                 R\xe9union   736 1.953441e-03
##        Saint Barth\xe9lemy     6 1.592479e-05
##               Saint Helena   609 1.616366e-03
##      Saint Kitts and Nevis   397 1.053690e-03
##                Saint Lucia   558 1.481006e-03
##   Saint Vincent/Grenadines   715 1.897704e-03
##                SaintMartin     6 1.592479e-05
##                      Samoa   386 1.024495e-03
##      Sao Tome and Principe  1035 2.747027e-03
##               Saudi Arabia  2200 5.839091e-03
##                    Senegal  2988 7.930547e-03
##      Serbia and Montenegro   516 1.369532e-03
##                 Seychelles  1142 3.031019e-03
##               Sierra Leone  1526 4.050206e-03
##                  Singapore  1937 5.141054e-03
##               Sint Maarten     4 1.061653e-05
##                   Slovenia   644 1.709261e-03
##            Solomon Islands   505 1.340337e-03
##                    Somalia   141 3.742326e-04
##               South Africa  3881 1.030069e-02
##                      Spain 17482 4.639954e-02
##                  Sri Lanka  1351 3.585732e-03
##    St. Pierre and Miquelon  1038 2.754989e-03
##                      Sudan     3 7.962396e-06
##             Sudan (former)    90 2.388719e-04
##                   Suriname   234 6.210669e-04
##     Svalbard and Jan Mayen    41 1.088194e-04
##                     Sweden  3115 8.267621e-03
##       Syrian Arab Republic   793 2.104727e-03
##   Taiwan Province of China  9927 2.634757e-02
##   Tanzania, United Rep. of  1277 3.389327e-03
##                   Thailand  4843 1.285396e-02
##                 TimorLeste    98 2.601049e-04
##                       Togo  1723 4.573070e-03
##                    Tokelau   102 2.707215e-04
##                      Tonga   403 1.069615e-03
##        Trinidad and Tobago   923 2.449764e-03
##                    Tunisia  3019 8.012825e-03
##                     Turkey  3326 8.827643e-03
##       Turks and Caicos Is.   193 5.122475e-04
##                     Tuvalu   162 4.299694e-04
##          US Virgin Islands   348 9.236380e-04
##                    Ukraine  1823 4.838483e-03
##         Un. Sov. Soc. Rep.  7084 1.880187e-02
##       United Arab Emirates  1801 4.780092e-03
##             United Kingdom  6577 1.745623e-02
##   United States of America 18080 4.798671e-02
##                    Uruguay  2134 5.663918e-03
##                    Vanuatu   789 2.094110e-03
##    Venezuela, Boliv Rep of  3409 9.047936e-03
##                   Viet Nam   405 1.074923e-03
##      Wallis and Futuna Is.   128 3.397289e-04
##                      Yemen  1278 3.391981e-03
##             Yugoslavia SFR  1383 3.670665e-03
##                   Zanzibar   247 6.555706e-04
```


4. Refocus the data only to include country, isscaap_taxonomic_group, asfis_species_name, asfis_species_number, year, catch.

```r
fisheries_tidy %>%
  select(country, isscaap_taxonomic_group, asfis_species_name, asfis_species_number, year, catch)
```

```
## # A tibble: 376,771 × 6
##    country isscaap_taxonomic_group asfis_species_name asfis_species_number  year
##    <chr>   <chr>                   <chr>              <chr>                <dbl>
##  1 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX            1995
##  2 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX            1996
##  3 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX            1997
##  4 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX            1998
##  5 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX            1999
##  6 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX            2000
##  7 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX            2001
##  8 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX            2002
##  9 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX            2003
## 10 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX            2004
## # ℹ 376,761 more rows
## # ℹ 1 more variable: catch <dbl>
```

5. Based on the asfis_species_number, how many distinct fish species were caught as part of these data?

```r
fisheries_tidy %>%
  summarize(n_asfisnumber=n_distinct(asfis_species_number))
```

```
## # A tibble: 1 × 1
##   n_asfisnumber
##           <int>
## 1          1551
```

6. Which country had the largest overall catch in the year 2000?

```r
fisheries_tidy %>%
  filter(year=="2000") %>%
  summarise(across(c(country, common_name, catch), max, na.rm=T))
```

```
## Warning: There was 1 warning in `summarise()`.
## ℹ In argument: `across(c(country, common_name, catch), max, na.rm = T)`.
## Caused by warning:
## ! The `...` argument of `across()` is deprecated as of dplyr 1.1.0.
## Supply arguments directly to `.fns` through an anonymous function instead.
## 
##   # Previously
##   across(a:b, mean, na.rm = TRUE)
## 
##   # Now
##   across(a:b, \(x) mean(x, na.rm = TRUE))
```

```
## # A tibble: 1 × 3
##   country  common_name   catch
##   <chr>    <chr>         <dbl>
## 1 Zanzibar Yesso scallop  9068
```


```r
fisheries_tidy %>% 
  filter(year=="2000") %>%
  summarize(max(catch, na.rm=T))
```

```
## # A tibble: 1 × 1
##   `max(catch, na.rm = T)`
##                     <dbl>
## 1                    9068
```

```r
fisheries_tidy %>%
  filter(catch=="9068")
```

```
## # A tibble: 1 × 10
##   country common_name       isscaap_group_number isscaap_taxonomic_group     
##   <chr>   <chr>                            <dbl> <chr>                       
## 1 China   Marine fishes nei                   39 Marine fishes not identified
## # ℹ 6 more variables: asfis_species_number <chr>, asfis_species_name <chr>,
## #   fao_major_fishing_area <dbl>, measure <chr>, year <dbl>, catch <dbl>
```


7. Which country caught the most sardines (_Sardina pilchardus_) between the years 1990-2000?




8. Which five countries caught the most cephalopods between 2008-2012?


9. Which species had the highest catch total between 2008-2012? (hint: Osteichthyes is not a species)


10. Use the data to do at least one analysis of your choice.

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
