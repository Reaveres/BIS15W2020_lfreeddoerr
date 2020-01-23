---
title: "Lab 2 Homework"
author: "Joel Ledford"
date: "Winter 2020"
output:
  html_document: 
    keep_md: yes
    theme: spacelab
---

## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to our [GitHub repository](https://github.com/FRS417-DataScienceBiologists). I will randomly select a few examples of student work at the start of each session to use as examples so be sure that your code is working to the best of your ability.

## Load the tidyverse


```r
library("tidyverse")
```

```
## <U+2500><U+2500> Attaching packages <U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500> tidyverse 1.3.0 <U+2500><U+2500>
```

```
## <U+2713> ggplot2 3.2.1     <U+2713> purrr   0.3.3
## <U+2713> tibble  2.1.3     <U+2713> dplyr   0.8.3
## <U+2713> tidyr   1.0.0     <U+2713> stringr 1.4.0
## <U+2713> readr   1.3.1     <U+2713> forcats 0.4.0
```

```
## <U+2500><U+2500> Conflicts <U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500><U+2500> tidyverse_conflicts() <U+2500><U+2500>
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

## Mammals Sleep
For this assignment, we are going to use built-in data on mammal sleep patterns.  

```r
msleep
```

```
## # A tibble: 83 x 11
##    name  genus vore  order conservation sleep_total sleep_rem sleep_cycle awake
##    <chr> <chr> <chr> <chr> <chr>              <dbl>     <dbl>       <dbl> <dbl>
##  1 Chee<U+2026> Acin<U+2026> carni Carn<U+2026> lc                  12.1      NA        NA      11.9
##  2 Owl <U+2026> Aotus omni  Prim<U+2026> <NA>                17         1.8      NA       7  
##  3 Moun<U+2026> Aplo<U+2026> herbi Rode<U+2026> nt                  14.4       2.4      NA       9.6
##  4 Grea<U+2026> Blar<U+2026> omni  Sori<U+2026> lc                  14.9       2.3       0.133   9.1
##  5 Cow   Bos   herbi Arti<U+2026> domesticated         4         0.7       0.667  20  
##  6 Thre<U+2026> Brad<U+2026> herbi Pilo<U+2026> <NA>                14.4       2.2       0.767   9.6
##  7 Nort<U+2026> Call<U+2026> carni Carn<U+2026> vu                   8.7       1.4       0.383  15.3
##  8 Vesp<U+2026> Calo<U+2026> <NA>  Rode<U+2026> <NA>                 7        NA        NA      17  
##  9 Dog   Canis carni Carn<U+2026> domesticated        10.1       2.9       0.333  13.9
## 10 Roe <U+2026> Capr<U+2026> herbi Arti<U+2026> lc                   3        NA        NA      21  
## # <U+2026> with 73 more rows, and 2 more variables: brainwt <dbl>, bodywt <dbl>
```

1. From which publication are these data taken from? Don't do an internet search; show the code that you would use to find out in R.

```r
?msleep
```
Taken from Proceedings of the National Academy of Sciences.

2. Put these data into a new object `sleep`. Make sure they are organized as a data frame.  

```r
sleep <- msleep
sleep
```

```
## # A tibble: 83 x 11
##    name  genus vore  order conservation sleep_total sleep_rem sleep_cycle awake
##    <chr> <chr> <chr> <chr> <chr>              <dbl>     <dbl>       <dbl> <dbl>
##  1 Chee<U+2026> Acin<U+2026> carni Carn<U+2026> lc                  12.1      NA        NA      11.9
##  2 Owl <U+2026> Aotus omni  Prim<U+2026> <NA>                17         1.8      NA       7  
##  3 Moun<U+2026> Aplo<U+2026> herbi Rode<U+2026> nt                  14.4       2.4      NA       9.6
##  4 Grea<U+2026> Blar<U+2026> omni  Sori<U+2026> lc                  14.9       2.3       0.133   9.1
##  5 Cow   Bos   herbi Arti<U+2026> domesticated         4         0.7       0.667  20  
##  6 Thre<U+2026> Brad<U+2026> herbi Pilo<U+2026> <NA>                14.4       2.2       0.767   9.6
##  7 Nort<U+2026> Call<U+2026> carni Carn<U+2026> vu                   8.7       1.4       0.383  15.3
##  8 Vesp<U+2026> Calo<U+2026> <NA>  Rode<U+2026> <NA>                 7        NA        NA      17  
##  9 Dog   Canis carni Carn<U+2026> domesticated        10.1       2.9       0.333  13.9
## 10 Roe <U+2026> Capr<U+2026> herbi Arti<U+2026> lc                   3        NA        NA      21  
## # <U+2026> with 73 more rows, and 2 more variables: brainwt <dbl>, bodywt <dbl>
```


3. Show a list of the column names is this data frame.

```r
names(sleep)
```

```
##  [1] "name"         "genus"        "vore"         "order"        "conservation"
##  [6] "sleep_total"  "sleep_rem"    "sleep_cycle"  "awake"        "brainwt"     
## [11] "bodywt"
```


4. Use `glimpse()` to summarize the data in `sleep`.

```r
glimpse(sleep)
```

```
## Observations: 83
## Variables: 11
## $ name         <chr> "Cheetah", "Owl monkey", "Mountain beaver", "Greater sho<U+2026>
## $ genus        <chr> "Acinonyx", "Aotus", "Aplodontia", "Blarina", "Bos", "Br<U+2026>
## $ vore         <chr> "carni", "omni", "herbi", "omni", "herbi", "herbi", "car<U+2026>
## $ order        <chr> "Carnivora", "Primates", "Rodentia", "Soricomorpha", "Ar<U+2026>
## $ conservation <chr> "lc", NA, "nt", "lc", "domesticated", NA, "vu", NA, "dom<U+2026>
## $ sleep_total  <dbl> 12.1, 17.0, 14.4, 14.9, 4.0, 14.4, 8.7, 7.0, 10.1, 3.0, <U+2026>
## $ sleep_rem    <dbl> NA, 1.8, 2.4, 2.3, 0.7, 2.2, 1.4, NA, 2.9, NA, 0.6, 0.8,<U+2026>
## $ sleep_cycle  <dbl> NA, NA, NA, 0.1333333, 0.6666667, 0.7666667, 0.3833333, <U+2026>
## $ awake        <dbl> 11.9, 7.0, 9.6, 9.1, 20.0, 9.6, 15.3, 17.0, 13.9, 21.0, <U+2026>
## $ brainwt      <dbl> NA, 0.01550, NA, 0.00029, 0.42300, NA, NA, NA, 0.07000, <U+2026>
## $ bodywt       <dbl> 50.000, 0.480, 1.350, 0.019, 600.000, 3.850, 20.490, 0.0<U+2026>
```


5. Use `summary()` to summarize the data in `sleep`.

```r
summary(sleep)
```

```
##      name              genus               vore              order          
##  Length:83          Length:83          Length:83          Length:83         
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##  conservation        sleep_total      sleep_rem      sleep_cycle    
##  Length:83          Min.   : 1.90   Min.   :0.100   Min.   :0.1167  
##  Class :character   1st Qu.: 7.85   1st Qu.:0.900   1st Qu.:0.1833  
##  Mode  :character   Median :10.10   Median :1.500   Median :0.3333  
##                     Mean   :10.43   Mean   :1.875   Mean   :0.4396  
##                     3rd Qu.:13.75   3rd Qu.:2.400   3rd Qu.:0.5792  
##                     Max.   :19.90   Max.   :6.600   Max.   :1.5000  
##                                     NA's   :22      NA's   :51      
##      awake          brainwt            bodywt        
##  Min.   : 4.10   Min.   :0.00014   Min.   :   0.005  
##  1st Qu.:10.25   1st Qu.:0.00290   1st Qu.:   0.174  
##  Median :13.90   Median :0.01240   Median :   1.670  
##  Mean   :13.57   Mean   :0.28158   Mean   : 166.136  
##  3rd Qu.:16.15   3rd Qu.:0.12550   3rd Qu.:  41.750  
##  Max.   :22.10   Max.   :5.71200   Max.   :6654.000  
##                  NA's   :27
```


6. Print out the first column of the data frame and then print out the first row.

```r
sleep$name
```

```
##  [1] "Cheetah"                        "Owl monkey"                    
##  [3] "Mountain beaver"                "Greater short-tailed shrew"    
##  [5] "Cow"                            "Three-toed sloth"              
##  [7] "Northern fur seal"              "Vesper mouse"                  
##  [9] "Dog"                            "Roe deer"                      
## [11] "Goat"                           "Guinea pig"                    
## [13] "Grivet"                         "Chinchilla"                    
## [15] "Star-nosed mole"                "African giant pouched rat"     
## [17] "Lesser short-tailed shrew"      "Long-nosed armadillo"          
## [19] "Tree hyrax"                     "North American Opossum"        
## [21] "Asian elephant"                 "Big brown bat"                 
## [23] "Horse"                          "Donkey"                        
## [25] "European hedgehog"              "Patas monkey"                  
## [27] "Western american chipmunk"      "Domestic cat"                  
## [29] "Galago"                         "Giraffe"                       
## [31] "Pilot whale"                    "Gray seal"                     
## [33] "Gray hyrax"                     "Human"                         
## [35] "Mongoose lemur"                 "African elephant"              
## [37] "Thick-tailed opposum"           "Macaque"                       
## [39] "Mongolian gerbil"               "Golden hamster"                
## [41] "Vole "                          "House mouse"                   
## [43] "Little brown bat"               "Round-tailed muskrat"          
## [45] "Slow loris"                     "Degu"                          
## [47] "Northern grasshopper mouse"     "Rabbit"                        
## [49] "Sheep"                          "Chimpanzee"                    
## [51] "Tiger"                          "Jaguar"                        
## [53] "Lion"                           "Baboon"                        
## [55] "Desert hedgehog"                "Potto"                         
## [57] "Deer mouse"                     "Phalanger"                     
## [59] "Caspian seal"                   "Common porpoise"               
## [61] "Potoroo"                        "Giant armadillo"               
## [63] "Rock hyrax"                     "Laboratory rat"                
## [65] "African striped mouse"          "Squirrel monkey"               
## [67] "Eastern american mole"          "Cotton rat"                    
## [69] "Mole rat"                       "Arctic ground squirrel"        
## [71] "Thirteen-lined ground squirrel" "Golden-mantled ground squirrel"
## [73] "Musk shrew"                     "Pig"                           
## [75] "Short-nosed echidna"            "Eastern american chipmunk"     
## [77] "Brazilian tapir"                "Tenrec"                        
## [79] "Tree shrew"                     "Bottle-nosed dolphin"          
## [81] "Genet"                          "Arctic fox"                    
## [83] "Red fox"
```

```r
sleep[1,]
```

```
## # A tibble: 1 x 11
##   name  genus vore  order conservation sleep_total sleep_rem sleep_cycle awake
##   <chr> <chr> <chr> <chr> <chr>              <dbl>     <dbl>       <dbl> <dbl>
## 1 Chee<U+2026> Acin<U+2026> carni Carn<U+2026> lc                  12.1        NA          NA  11.9
## # <U+2026> with 2 more variables: brainwt <dbl>, bodywt <dbl>
```


7. We are interested in two groups; small and large mammals. Let's define small as less than or equal to 1kg body weight and large as greater than or equal to 200kg body weight. Make two new dataframes (large and small) based on these parameters.  

```r
large_mammal <- subset.data.frame(sleep, bodywt >= 200)
large_mammal
```

```
## # A tibble: 7 x 11
##   name  genus vore  order conservation sleep_total sleep_rem sleep_cycle awake
##   <chr> <chr> <chr> <chr> <chr>              <dbl>     <dbl>       <dbl> <dbl>
## 1 Cow   Bos   herbi Arti<U+2026> domesticated         4         0.7       0.667  20  
## 2 Asia<U+2026> Elep<U+2026> herbi Prob<U+2026> en                   3.9      NA        NA      20.1
## 3 Horse Equus herbi Peri<U+2026> domesticated         2.9       0.6       1      21.1
## 4 Gira<U+2026> Gira<U+2026> herbi Arti<U+2026> cd                   1.9       0.4      NA      22.1
## 5 Pilo<U+2026> Glob<U+2026> carni Ceta<U+2026> cd                   2.7       0.1      NA      21.4
## 6 Afri<U+2026> Loxo<U+2026> herbi Prob<U+2026> vu                   3.3      NA        NA      20.7
## 7 Braz<U+2026> Tapi<U+2026> herbi Peri<U+2026> vu                   4.4       1         0.9    19.6
## # <U+2026> with 2 more variables: brainwt <dbl>, bodywt <dbl>
```

```r
sm_mammal <- subset.data.frame(sleep, bodywt <= 1)
sm_mammal
```

```
## # A tibble: 36 x 11
##    name  genus vore  order conservation sleep_total sleep_rem sleep_cycle awake
##    <chr> <chr> <chr> <chr> <chr>              <dbl>     <dbl>       <dbl> <dbl>
##  1 Owl <U+2026> Aotus omni  Prim<U+2026> <NA>                17         1.8      NA       7  
##  2 Grea<U+2026> Blar<U+2026> omni  Sori<U+2026> lc                  14.9       2.3       0.133   9.1
##  3 Vesp<U+2026> Calo<U+2026> <NA>  Rode<U+2026> <NA>                 7        NA        NA      17  
##  4 Guin<U+2026> Cavis herbi Rode<U+2026> domesticated         9.4       0.8       0.217  14.6
##  5 Chin<U+2026> Chin<U+2026> herbi Rode<U+2026> domesticated        12.5       1.5       0.117  11.5
##  6 Star<U+2026> Cond<U+2026> omni  Sori<U+2026> lc                  10.3       2.2      NA      13.7
##  7 Afri<U+2026> Cric<U+2026> omni  Rode<U+2026> <NA>                 8.3       2        NA      15.7
##  8 Less<U+2026> Cryp<U+2026> omni  Sori<U+2026> lc                   9.1       1.4       0.15   14.9
##  9 Big <U+2026> Epte<U+2026> inse<U+2026> Chir<U+2026> lc                  19.7       3.9       0.117   4.3
## 10 Euro<U+2026> Erin<U+2026> omni  Erin<U+2026> lc                  10.1       3.5       0.283  13.9
## # <U+2026> with 26 more rows, and 2 more variables: brainwt <dbl>, bodywt <dbl>
```

8. What is the mean weight for both the large and small mammals?

```r
large_mean <- mean(large_mammal$bodywt)
small_mean <- mean(sm_mammal$bodywt)
```


9. Let's try to figure out if large mammals sleep, on average, longer than small mammals. What is the average sleep duration for large mammals as we have defined them?
10. What is the average sleep duration for small mammals as we have defined them?

```r
l_sleep <- mean(large_mammal$sleep_total)
s_sleep <- mean(sm_mammal$sleep_total)
```

11. Which animals are the sleepiest? Which sleep least 18 hours per day?  

```r
if(l_sleep>s_sleep) {  
  print("large mammals sleep more") 
} else {
  print("small mammals sleep more") 
}
```

```
## [1] "small mammals sleep more"
```

```r
sleepy_friends <- subset.data.frame(sleep, sleep_total >= 18)
sleepy_friends
```

```
## # A tibble: 5 x 11
##   name  genus vore  order conservation sleep_total sleep_rem sleep_cycle awake
##   <chr> <chr> <chr> <chr> <chr>              <dbl>     <dbl>       <dbl> <dbl>
## 1 Nort<U+2026> Dide<U+2026> omni  Dide<U+2026> lc                  18         4.9       0.333   6  
## 2 Big <U+2026> Epte<U+2026> inse<U+2026> Chir<U+2026> lc                  19.7       3.9       0.117   4.3
## 3 Thic<U+2026> Lutr<U+2026> carni Dide<U+2026> lc                  19.4       6.6      NA       4.6
## 4 Litt<U+2026> Myot<U+2026> inse<U+2026> Chir<U+2026> <NA>                19.9       2         0.2     4.1
## 5 Gian<U+2026> Prio<U+2026> inse<U+2026> Cing<U+2026> en                  18.1       6.1      NA       5.9
## # <U+2026> with 2 more variables: brainwt <dbl>, bodywt <dbl>
```


## Push your final code to GitHub
