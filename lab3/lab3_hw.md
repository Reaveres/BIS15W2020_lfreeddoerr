---
title: "Lab 3 Homework"
author: "Lia Freed-Doerr"
date: "Winter 2020"
output:
  html_document: 
    keep_md: yes
    theme: spacelab
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run.  

## Load the tidyverse

```r
library(tidyverse)
```

## Data
For the homework, we will use data about vertebrate home range sizes. The data are in the class folder, but the reference is below.  

**Database of vertebrate home range sizes.**  
Reference: Tamburello N, Cote IM, Dulvy NK (2015) Energy and the scaling of animal space use. The American Naturalist 186(2):196-211. http://dx.doi.org/10.1086/682070.  
Data: http://datadryad.org/resource/doi:10.5061/dryad.q5j65/1  

1. Load the data into a new object called `homerange`.  

```r
homerange <- readr::read_csv("doi_10.5061_dryad.q5j65__v1/Tamburelloetal_HomeRangeDatabase.csv")
```

```
## Parsed with column specification:
## cols(
##   .default = col_character(),
##   mean.mass.g = col_double(),
##   log10.mass = col_double(),
##   mean.hra.m2 = col_double(),
##   log10.hra = col_double(),
##   preymass = col_double(),
##   log10.preymass = col_double(),
##   PPMR = col_double()
## )
```

```
## See spec(...) for full column specifications.
```


2. Use `spec()` to see the full details of the columns.  

```r
spec(homerange)
```

```
## cols(
##   taxon = col_character(),
##   common.name = col_character(),
##   class = col_character(),
##   order = col_character(),
##   family = col_character(),
##   genus = col_character(),
##   species = col_character(),
##   primarymethod = col_character(),
##   N = col_character(),
##   mean.mass.g = col_double(),
##   log10.mass = col_double(),
##   alternative.mass.reference = col_character(),
##   mean.hra.m2 = col_double(),
##   log10.hra = col_double(),
##   hra.reference = col_character(),
##   realm = col_character(),
##   thermoregulation = col_character(),
##   locomotion = col_character(),
##   trophic.guild = col_character(),
##   dimension = col_character(),
##   preymass = col_double(),
##   log10.preymass = col_double(),
##   PPMR = col_double(),
##   prey.size.reference = col_character()
## )
```


3. Explore the data. Show the dimensions, column names, classes for each variable, and a statistical summary. Keep these as separate code chunks.  

```r
dim(homerange)
```

```
## [1] 569  24
```


```r
names(homerange)
```

```
##  [1] "taxon"                      "common.name"               
##  [3] "class"                      "order"                     
##  [5] "family"                     "genus"                     
##  [7] "species"                    "primarymethod"             
##  [9] "N"                          "mean.mass.g"               
## [11] "log10.mass"                 "alternative.mass.reference"
## [13] "mean.hra.m2"                "log10.hra"                 
## [15] "hra.reference"              "realm"                     
## [17] "thermoregulation"           "locomotion"                
## [19] "trophic.guild"              "dimension"                 
## [21] "preymass"                   "log10.preymass"            
## [23] "PPMR"                       "prey.size.reference"
```


```r
str(homerange)
```

```
## Classes 'spec_tbl_df', 'tbl_df', 'tbl' and 'data.frame':	569 obs. of  24 variables:
##  $ taxon                     : chr  "lake fishes" "river fishes" "river fishes" "river fishes" ...
##  $ common.name               : chr  "american eel" "blacktail redhorse" "central stoneroller" "rosyside dace" ...
##  $ class                     : chr  "actinopterygii" "actinopterygii" "actinopterygii" "actinopterygii" ...
##  $ order                     : chr  "anguilliformes" "cypriniformes" "cypriniformes" "cypriniformes" ...
##  $ family                    : chr  "anguillidae" "catostomidae" "cyprinidae" "cyprinidae" ...
##  $ genus                     : chr  "anguilla" "moxostoma" "campostoma" "clinostomus" ...
##  $ species                   : chr  "rostrata" "poecilura" "anomalum" "funduloides" ...
##  $ primarymethod             : chr  "telemetry" "mark-recapture" "mark-recapture" "mark-recapture" ...
##  $ N                         : chr  "16" NA "20" "26" ...
##  $ mean.mass.g               : num  887 562 34 4 4 ...
##  $ log10.mass                : num  2.948 2.75 1.531 0.602 0.602 ...
##  $ alternative.mass.reference: chr  NA NA NA NA ...
##  $ mean.hra.m2               : num  282750 282.1 116.1 125.5 87.1 ...
##  $ log10.hra                 : num  5.45 2.45 2.06 2.1 1.94 ...
##  $ hra.reference             : chr  "Minns, C. K. 1995. Allometry of home range size in lake and river fishes. Canadian Journal of Fisheries and Aqu"| __truncated__ "Minns, C. K. 1995. Allometry of home range size in lake and river fishes. Canadian Journal of Fisheries and Aqu"| __truncated__ "Minns, C. K. 1995. Allometry of home range size in lake and river fishes. Canadian Journal of Fisheries and Aqu"| __truncated__ "Minns, C. K. 1995. Allometry of home range size in lake and river fishes. Canadian Journal of Fisheries and Aqu"| __truncated__ ...
##  $ realm                     : chr  "aquatic" "aquatic" "aquatic" "aquatic" ...
##  $ thermoregulation          : chr  "ectotherm" "ectotherm" "ectotherm" "ectotherm" ...
##  $ locomotion                : chr  "swimming" "swimming" "swimming" "swimming" ...
##  $ trophic.guild             : chr  "carnivore" "carnivore" "carnivore" "carnivore" ...
##  $ dimension                 : chr  "3D" "2D" "2D" "2D" ...
##  $ preymass                  : num  NA NA NA NA NA NA 1.39 NA NA NA ...
##  $ log10.preymass            : num  NA NA NA NA NA ...
##  $ PPMR                      : num  NA NA NA NA NA NA 530 NA NA NA ...
##  $ prey.size.reference       : chr  NA NA NA NA ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   taxon = col_character(),
##   ..   common.name = col_character(),
##   ..   class = col_character(),
##   ..   order = col_character(),
##   ..   family = col_character(),
##   ..   genus = col_character(),
##   ..   species = col_character(),
##   ..   primarymethod = col_character(),
##   ..   N = col_character(),
##   ..   mean.mass.g = col_double(),
##   ..   log10.mass = col_double(),
##   ..   alternative.mass.reference = col_character(),
##   ..   mean.hra.m2 = col_double(),
##   ..   log10.hra = col_double(),
##   ..   hra.reference = col_character(),
##   ..   realm = col_character(),
##   ..   thermoregulation = col_character(),
##   ..   locomotion = col_character(),
##   ..   trophic.guild = col_character(),
##   ..   dimension = col_character(),
##   ..   preymass = col_double(),
##   ..   log10.preymass = col_double(),
##   ..   PPMR = col_double(),
##   ..   prey.size.reference = col_character()
##   .. )
```


```r
summary(homerange)
```

```
##     taxon           common.name           class              order          
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##     family             genus             species          primarymethod     
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##       N              mean.mass.g        log10.mass     
##  Length:569         Min.   :      0   Min.   :-0.6576  
##  Class :character   1st Qu.:     50   1st Qu.: 1.6990  
##  Mode  :character   Median :    330   Median : 2.5185  
##                     Mean   :  34602   Mean   : 2.5947  
##                     3rd Qu.:   2150   3rd Qu.: 3.3324  
##                     Max.   :4000000   Max.   : 6.6021  
##                                                        
##  alternative.mass.reference  mean.hra.m2          log10.hra     
##  Length:569                 Min.   :0.000e+00   Min.   :-1.523  
##  Class :character           1st Qu.:4.500e+03   1st Qu.: 3.653  
##  Mode  :character           Median :3.934e+04   Median : 4.595  
##                             Mean   :2.146e+07   Mean   : 4.709  
##                             3rd Qu.:1.038e+06   3rd Qu.: 6.016  
##                             Max.   :3.551e+09   Max.   : 9.550  
##                                                                 
##  hra.reference         realm           thermoregulation    locomotion       
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##  trophic.guild       dimension            preymass         log10.preymass   
##  Length:569         Length:569         Min.   :     0.67   Min.   :-0.1739  
##  Class :character   Class :character   1st Qu.:    20.02   1st Qu.: 1.3014  
##  Mode  :character   Mode  :character   Median :    53.75   Median : 1.7304  
##                                        Mean   :  3989.88   Mean   : 2.0188  
##                                        3rd Qu.:   363.35   3rd Qu.: 2.5603  
##                                        Max.   :130233.20   Max.   : 5.1147  
##                                        NA's   :502         NA's   :502      
##       PPMR         prey.size.reference
##  Min.   :  0.380   Length:569         
##  1st Qu.:  3.315   Class :character   
##  Median :  7.190   Mode  :character   
##  Mean   : 31.752                      
##  3rd Qu.: 15.966                      
##  Max.   :530.000                      
##  NA's   :502
```

4. Are there NA's in your data? Show the code that you would use to verify this, please.  

```r
anyNA(homerange)
```

```
## [1] TRUE
```

5. Change the class of the variables `taxon` and `order` to factors and display their levels.  

```r
levels(as.factor(homerange$taxon))
```

```
## [1] "birds"         "lake fishes"   "lizards"       "mammals"      
## [5] "marine fishes" "river fishes"  "snakes"        "tortoises"    
## [9] "turtles"
```


```r
levels(as.factor(homerange$order))
```

```
##  [1] "accipitriformes"         "afrosoricida"           
##  [3] "anguilliformes"          "anseriformes"           
##  [5] "apterygiformes"          "artiodactyla"           
##  [7] "caprimulgiformes"        "carnivora"              
##  [9] "charadriiformes"         "columbidormes"          
## [11] "columbiformes"           "coraciiformes"          
## [13] "cuculiformes"            "cypriniformes"          
## [15] "dasyuromorpha"           "dasyuromorpia"          
## [17] "didelphimorphia"         "diprodontia"            
## [19] "diprotodontia"           "erinaceomorpha"         
## [21] "esociformes"             "falconiformes"          
## [23] "gadiformes"              "galliformes"            
## [25] "gruiformes"              "lagomorpha"             
## [27] "macroscelidea"           "monotrematae"           
## [29] "passeriformes"           "pelecaniformes"         
## [31] "peramelemorphia"         "perciformes"            
## [33] "perissodactyla"          "piciformes"             
## [35] "pilosa"                  "proboscidea"            
## [37] "psittaciformes"          "rheiformes"             
## [39] "roden"                   "rodentia"               
## [41] "salmoniformes"           "scorpaeniformes"        
## [43] "siluriformes"            "soricomorpha"           
## [45] "squamata"                "strigiformes"           
## [47] "struthioniformes"        "syngnathiformes"        
## [49] "testudines"              "tetraodontiformes<U+00A0>"
## [51] "tinamiformes"
```

6. Make a new dataframe `deer` that is limited to the mean mass, log10 mass, family, genus, and species of deer in the database. The family for deer is cervidae. Arrange the data in descending order by log10 mass. Which is the largest deer?  

```r
deer <- homerange %>%
  select(mean.mass.g, log10.mass, family, genus, species) %>%
  filter(family == "cervidae")
```


```r
deer %>% arrange(desc(log10.mass))
```

```
## # A tibble: 12 x 5
##    mean.mass.g log10.mass family   genus      species    
##          <dbl>      <dbl> <chr>    <chr>      <chr>      
##  1     307227.       5.49 cervidae alces      alces      
##  2     234758.       5.37 cervidae cervus     elaphus    
##  3     102059.       5.01 cervidae rangifer   tarandus   
##  4      87884.       4.94 cervidae odocoileus virginianus
##  5      71450.       4.85 cervidae dama       dama       
##  6      62823.       4.80 cervidae axis       axis       
##  7      53864.       4.73 cervidae odocoileus hemionus   
##  8      35000.       4.54 cervidae ozotoceros bezoarticus
##  9      29450.       4.47 cervidae cervus     nippon     
## 10      24050.       4.38 cervidae capreolus  capreolus  
## 11      13500.       4.13 cervidae muntiacus  reevesi    
## 12       7500.       3.88 cervidae pudu       puda
```

+ alces is the largest deer

7. As measured by the data, which snake species has the smallest homerange? Show all of your work, please. Look this species up online and tell me about it!  

```r
snakes <- homerange %>%
  filter(taxon == "snakes")
snakes %>% arrange(log10.hra)
```

```
## # A tibble: 41 x 24
##    taxon common.name class order family genus species primarymethod N    
##    <chr> <chr>       <chr> <chr> <chr>  <chr> <chr>   <chr>         <chr>
##  1 snak<U+2026> namaqua dw<U+2026> rept<U+2026> squa<U+2026> viper<U+2026> bitis schnei<U+2026> telemetry     11   
##  2 snak<U+2026> eastern wo<U+2026> rept<U+2026> squa<U+2026> colub<U+2026> carp<U+2026> viridis radiotag      10   
##  3 snak<U+2026> butlers ga<U+2026> rept<U+2026> squa<U+2026> colub<U+2026> tham<U+2026> butleri mark-recaptu<U+2026> 1    
##  4 snak<U+2026> western wo<U+2026> rept<U+2026> squa<U+2026> colub<U+2026> carp<U+2026> vermis  radiotag      1    
##  5 snak<U+2026> snubnosed <U+2026> rept<U+2026> squa<U+2026> viper<U+2026> vipe<U+2026> latast<U+2026> telemetry     7    
##  6 snak<U+2026> chinese pi<U+2026> rept<U+2026> squa<U+2026> viper<U+2026> gloy<U+2026> shedao<U+2026> telemetry     16   
##  7 snak<U+2026> ringneck s<U+2026> rept<U+2026> squa<U+2026> colub<U+2026> diad<U+2026> puncta<U+2026> mark-recaptu<U+2026> <NA> 
##  8 snak<U+2026> cottonmouth rept<U+2026> squa<U+2026> viper<U+2026> agki<U+2026> pisciv<U+2026> telemetry     15   
##  9 snak<U+2026> redbacked <U+2026> rept<U+2026> squa<U+2026> colub<U+2026> ooca<U+2026> rufodo<U+2026> telemetry     21   
## 10 snak<U+2026> gopher sna<U+2026> rept<U+2026> squa<U+2026> colub<U+2026> pitu<U+2026> cateni<U+2026> telemetry     4    
## # <U+2026> with 31 more rows, and 15 more variables: mean.mass.g <dbl>,
## #   log10.mass <dbl>, alternative.mass.reference <chr>, mean.hra.m2 <dbl>,
## #   log10.hra <dbl>, hra.reference <chr>, realm <chr>, thermoregulation <chr>,
## #   locomotion <chr>, trophic.guild <chr>, dimension <chr>, preymass <dbl>,
## #   log10.preymass <dbl>, PPMR <dbl>, prey.size.reference <chr>
```
+ the namaqua dwarf adder has the smallest homerange as measured by log10.hra.
+ it is the smallest venomous viper, generally between 7-10 inches, and comes from South Africa.
+ (wikipedia)

8. You suspect that homerange and mass are correlated in birds. We need a ratio that facilitates exploration of this prediction. First, build a new dataframe called `hra_ratio` that is limited to genus, species, mean.mass.g, log10.mass, log10.hra. Arrange it in ascending order by mean mass in grams.  

```r
hra_ratio <- homerange %>%
  select(genus, species, taxon, mean.mass.g, log10.mass, log10.hra) %>%
  arrange(mean.mass.g)
hra_ratio
```

```
## # A tibble: 569 x 6
##    genus          species        taxon         mean.mass.g log10.mass log10.hra
##    <chr>          <chr>          <chr>               <dbl>      <dbl>     <dbl>
##  1 priolepis      hipoliti       marine fishes        0.22    -0.658    -1.52  
##  2 lythrypnus     dalli          marine fishes        0.31    -0.509    -0.301 
##  3 amblycirrhitus pinos          marine fishes        0.45    -0.347     0.405 
##  4 nerophis       lumbriciformis marine fishes        1.22     0.0864    1.10  
##  5 salmo          salar          river fishes         2        0.301     1.65  
##  6 centropyge     argi           marine fishes        2.5      0.398     0.0531
##  7 amblyeleotris  japonica       marine fishes        2.7      0.431     1.45  
##  8 cottus         carolinae      river fishes         3        0.477     1.67  
##  9 thalassoma     bifasciatum    marine fishes        3.12     0.494     2.01  
## 10 carphopis      vermis         snakes               3.46     0.539     2.85  
## # <U+2026> with 559 more rows
```


9. Replace the existing `hra_ratio` dataframe with a new dataframe that adds a column calculating the ratio of log 10 hra to log 10 mass. Call it `hra.mass.ratio`. Arrange it in descending order by mean mass in grams.  

```r
hra_ratio <- hra_ratio %>% 
  mutate(hra.mass.ratio = log10.hra/log10.mass) %>%
  arrange(desc(mean.mass.g))
hra_ratio
```

```
## # A tibble: 569 x 7
##    genus      species     taxon  mean.mass.g log10.mass log10.hra hra.mass.ratio
##    <chr>      <chr>       <chr>        <dbl>      <dbl>     <dbl>          <dbl>
##  1 elephas    maximus     mamma<U+2026>    4000000.       6.60      8.04           1.22
##  2 loxodonta  africana    mamma<U+2026>    4000000.       6.60      9.24           1.40
##  3 ceratothe<U+2026> simum       mamma<U+2026>    2249987.       6.35      7.20           1.13
##  4 giraffa    camelopard<U+2026> mamma<U+2026>    1339985.       6.13      8.14           1.33
##  5 diceros    bicornis    mamma<U+2026>    1050002.       6.02      7.62           1.27
##  6 taurotrag<U+2026> oryx        mamma<U+2026>     635038.       5.80      7.72           1.33
##  7 bison      bison       mamma<U+2026>     629999.       5.80      8.42           1.45
##  8 oreamnos   americanus  mamma<U+2026>     629999.       5.80      7.37           1.27
##  9 bison      bonasus     mamma<U+2026>     628001.       5.80      7.01           1.21
## 10 equus      caballus    mamma<U+2026>     427996.       5.63      7.35           1.30
## # <U+2026> with 559 more rows
```


10. What is the lowest mass for birds with a `hra.mass.ratio` greater than or equal to 4.0?

```r
hra_ratio %>% filter(hra.mass.ratio >= 4.0 & taxon == "birds")
```

```
## # A tibble: 17 x 7
##    genus       species     taxon mean.mass.g log10.mass log10.hra hra.mass.ratio
##    <chr>       <chr>       <chr>       <dbl>      <dbl>     <dbl>          <dbl>
##  1 motacilla   alba        birds       21.2       1.33       5.89           4.44
##  2 contopus    virens      birds       13.8       1.14       4.64           4.07
##  3 spizella    passerina   birds       12.2       1.09       4.49           4.13
##  4 hippolais   polyglotta  birds       11         1.04       4.48           4.30
##  5 parus       palustris   birds       11         1.04       4.36           4.18
##  6 parus       carolinens<U+2026> birds       10.1       1.00       4.18           4.16
##  7 vireo       belli       birds       10         1          4.07           4.07
##  8 cisticola   juncidis    birds        9.8       0.991      4.16           4.20
##  9 troglodytes troglodytes birds        9.5       0.978      4.01           4.10
## 10 wilsonia    canadensis  birds        9.3       0.968      4.01           4.14
## 11 certhia     familiaris  birds        8.77      0.943      4.67           4.95
## 12 setophaga   magnolia    birds        8.6       0.934      3.86           4.13
## 13 vireo       atricapill<U+2026> birds        8.5       0.929      4.18           4.49
## 14 aegithalos  caudatus    birds        8         0.903      4.62           5.12
## 15 phylloscop<U+2026> bonelli     birds        7.5       0.875      4.54           5.19
## 16 regulus     ignicapill<U+2026> birds        5.3       0.724      4.22           5.82
## 17 regulus     regulus     birds        5.15      0.712      4.30           6.04
```
+ the regulus regulus is the lowest mass bird with homerange >= 4

11. Do a search online; what is the common name of the bird from #8 above? Place a link in your markdown file that takes us to a webpage with information on its biology.  
+ this bird is known as the goldcrest
+ [Goldcrest Wikipedia](https://en.wikipedia.org/wiki/Goldcrest)

12. What is the `hra.mass.ratio` for an ostrich? Show your work, please.  

```r
homerange %>% filter(common.name == "ostrich") %>%
  select(genus, species)
```

```
## # A tibble: 1 x 2
##   genus    species
##   <chr>    <chr>  
## 1 struthio camelus
```
+ tells us genus and species of ostrich: struthio and camelus: 
+ allows selection in hra_ratio


```r
ratio_ostrich <- hra_ratio %>% 
  filter(genus == "struthio" & species == "camelus") %>%
  select(hra.mass.ratio)
ratio_ostrich
```

```
## # A tibble: 1 x 1
##   hra.mass.ratio
##            <dbl>
## 1           1.60
```

+ hra.mass.ratio for ostrich is 1.602565

## Push your final code to GitHub!
Please be sure that you have check the `keep md` file in the knit preferences.  
