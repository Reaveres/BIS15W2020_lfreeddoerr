---
title: "Lab 4 Homework"
author: "Lia Freed-Doerr"
date: "2/7"
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

For this assignment we are going to work with a large dataset from the [United Nations Food and Agriculture Organization](http://www.fao.org/about/en/) on world fisheries. First, load the data.  

1. Load the data `FAO_1950to2012_111914.csv` as a new object titled `fisheries`.

```r
fisheries <- readr::read_csv("data/FAO_1950to2012_111914.csv")
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
##    Country `Common name` `ISSCAAP group#` `ISSCAAP taxono~ `ASFIS species#`
##    <chr>   <chr>                    <dbl> <chr>            <chr>           
##  1 Albania Angelsharks,~               38 Sharks, rays, c~ 10903XXXXX      
##  2 Albania Atlantic bon~               36 Tunas, bonitos,~ 1750100101      
##  3 Albania Barracudas n~               37 Miscellaneous p~ 17710001XX      
##  4 Albania Blue and red~               45 Shrimps, prawns  2280203101      
##  5 Albania Blue whiting~               32 Cods, hakes, ha~ 1480403301      
##  6 Albania Bluefish                    37 Miscellaneous p~ 1702021301      
##  7 Albania Bogue                       33 Miscellaneous c~ 1703926101      
##  8 Albania Caramote pra~               45 Shrimps, prawns  2280100117      
##  9 Albania Catsharks, n~               38 Sharks, rays, c~ 10801003XX      
## 10 Albania Common cuttl~               57 Squids, cuttlef~ 3210200202      
## # ... with 17,682 more rows, and 66 more variables: `ASFIS species name` <chr>,
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
names(fisheries)
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
+ Ah! The years are column names and should be variables.

3. What is the structure of the data? Show the classes of each variable.

```r
lapply(fisheries, class)
```

```
## $Country
## [1] "character"
## 
## $`Common name`
## [1] "character"
## 
## $`ISSCAAP group#`
## [1] "numeric"
## 
## $`ISSCAAP taxonomic group`
## [1] "character"
## 
## $`ASFIS species#`
## [1] "character"
## 
## $`ASFIS species name`
## [1] "character"
## 
## $`FAO major fishing area`
## [1] "numeric"
## 
## $Measure
## [1] "character"
## 
## $`1950`
## [1] "character"
## 
## $`1951`
## [1] "character"
## 
## $`1952`
## [1] "character"
## 
## $`1953`
## [1] "character"
## 
## $`1954`
## [1] "character"
## 
## $`1955`
## [1] "character"
## 
## $`1956`
## [1] "character"
## 
## $`1957`
## [1] "character"
## 
## $`1958`
## [1] "character"
## 
## $`1959`
## [1] "character"
## 
## $`1960`
## [1] "character"
## 
## $`1961`
## [1] "character"
## 
## $`1962`
## [1] "character"
## 
## $`1963`
## [1] "character"
## 
## $`1964`
## [1] "character"
## 
## $`1965`
## [1] "character"
## 
## $`1966`
## [1] "character"
## 
## $`1967`
## [1] "character"
## 
## $`1968`
## [1] "character"
## 
## $`1969`
## [1] "character"
## 
## $`1970`
## [1] "character"
## 
## $`1971`
## [1] "character"
## 
## $`1972`
## [1] "character"
## 
## $`1973`
## [1] "character"
## 
## $`1974`
## [1] "character"
## 
## $`1975`
## [1] "character"
## 
## $`1976`
## [1] "character"
## 
## $`1977`
## [1] "character"
## 
## $`1978`
## [1] "character"
## 
## $`1979`
## [1] "character"
## 
## $`1980`
## [1] "character"
## 
## $`1981`
## [1] "character"
## 
## $`1982`
## [1] "character"
## 
## $`1983`
## [1] "character"
## 
## $`1984`
## [1] "character"
## 
## $`1985`
## [1] "character"
## 
## $`1986`
## [1] "character"
## 
## $`1987`
## [1] "character"
## 
## $`1988`
## [1] "character"
## 
## $`1989`
## [1] "character"
## 
## $`1990`
## [1] "character"
## 
## $`1991`
## [1] "character"
## 
## $`1992`
## [1] "character"
## 
## $`1993`
## [1] "character"
## 
## $`1994`
## [1] "character"
## 
## $`1995`
## [1] "character"
## 
## $`1996`
## [1] "character"
## 
## $`1997`
## [1] "character"
## 
## $`1998`
## [1] "character"
## 
## $`1999`
## [1] "character"
## 
## $`2000`
## [1] "character"
## 
## $`2001`
## [1] "character"
## 
## $`2002`
## [1] "character"
## 
## $`2003`
## [1] "character"
## 
## $`2004`
## [1] "character"
## 
## $`2005`
## [1] "character"
## 
## $`2006`
## [1] "character"
## 
## $`2007`
## [1] "character"
## 
## $`2008`
## [1] "character"
## 
## $`2009`
## [1] "character"
## 
## $`2010`
## [1] "character"
## 
## $`2011`
## [1] "character"
## 
## $`2012`
## [1] "character"
```

4. Think about the classes. Will any present problems? Make any changes you think are necessary below.
+ The year variables and possibly ASFIS species # ought to be numeric, but the extra letters must be removed.
+ The other variables should be factors, not characters.

```r
fisheries <- fisheries %>% mutate_all(~str_remove_all(., " F")) %>%
  mutate_all(str_trim) %>%
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
fisheries
```

```
## # A tibble: 17,692 x 71
##    Country `Common name` `ISSCAAP group#` `ISSCAAP taxono~ `ASFIS species#`
##    <fct>   <fct>         <fct>            <fct>            <fct>           
##  1 Albania Angelsharks,~ 38               Sharks, rays, c~ 10903XXXXX      
##  2 Albania Atlantic bon~ 36               Tunas, bonitos,~ 1750100101      
##  3 Albania Barracudas n~ 37               Miscellaneous p~ 17710001XX      
##  4 Albania Blue and red~ 45               Shrimps, prawns  2280203101      
##  5 Albania Blue whiting~ 32               Cods, hakes, ha~ 1480403301      
##  6 Albania Bluefish      37               Miscellaneous p~ 1702021301      
##  7 Albania Bogue         33               Miscellaneous c~ 1703926101      
##  8 Albania Caramote pra~ 45               Shrimps, prawns  2280100117      
##  9 Albania Catsharks, n~ 38               Sharks, rays, c~ 10801003XX      
## 10 Albania Common cuttl~ 57               Squids, cuttlef~ 3210200202      
## # ... with 17,682 more rows, and 66 more variables: `ASFIS species name` <fct>,
## #   `FAO major fishing area` <fct>, Measure <fct>, `1950` <dbl>, `1951` <dbl>,
## #   `1952` <dbl>, `1953` <dbl>, `1954` <dbl>, `1955` <dbl>, `1956` <dbl>,
## #   `1957` <dbl>, `1958` <dbl>, `1959` <dbl>, `1960` <dbl>, `1961` <dbl>,
## #   `1962` <dbl>, `1963` <dbl>, `1964` <dbl>, `1965` <dbl>, `1966` <dbl>,
## #   `1967` <dbl>, `1968` <dbl>, `1969` <dbl>, `1970` <dbl>, `1971` <dbl>,
## #   `1972` <dbl>, `1973` <dbl>, `1974` <dbl>, `1975` <dbl>, `1976` <dbl>,
## #   `1977` <dbl>, `1978` <dbl>, `1979` <dbl>, `1980` <dbl>, `1981` <dbl>,
## #   `1982` <dbl>, `1983` <dbl>, `1984` <dbl>, `1985` <dbl>, `1986` <dbl>,
## #   `1987` <dbl>, `1988` <dbl>, `1989` <dbl>, `1990` <dbl>, `1991` <dbl>,
## #   `1992` <dbl>, `1993` <dbl>, `1994` <dbl>, `1995` <dbl>, `1996` <dbl>,
## #   `1997` <dbl>, `1998` <dbl>, `1999` <dbl>, `2000` <dbl>, `2001` <dbl>,
## #   `2002` <dbl>, `2003` <dbl>, `2004` <dbl>, `2005` <dbl>, `2006` <dbl>,
## #   `2007` <dbl>, `2008` <dbl>, `2009` <dbl>, `2010` <dbl>, `2011` <dbl>,
## #   `2012` <dbl>
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
fisheries %>% count(Country)
```

```
## # A tibble: 204 x 2
##    Country                 n
##    <fct>               <int>
##  1 Albania                67
##  2 Algeria                59
##  3 American Samoa         32
##  4 Angola                 88
##  5 Anguilla                3
##  6 Antigua and Barbuda    22
##  7 Argentina             140
##  8 Aruba                   5
##  9 Australia             301
## 10 Bahamas                14
## # ... with 194 more rows
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
fisheries <- fisheries %>% dplyr::rename(
  country='Country',
  commname='Common name',
  ASFIS_sciname='ASFIS species name',
  ASFIS_spcode='ASFIS species#',
  ISSCAAP_spgroup='ISSCAAP group#',
  ISSCAAP_spgroupname='ISSCAAP taxonomic group'
)
fisheries
```

```
## # A tibble: 17,692 x 71
##    country commname ISSCAAP_spgroup ISSCAAP_spgroup~ ASFIS_spcode ASFIS_sciname
##    <fct>   <fct>    <fct>           <fct>            <fct>        <fct>        
##  1 Albania Angelsh~ 38              Sharks, rays, c~ 10903XXXXX   Squatinidae  
##  2 Albania Atlanti~ 36              Tunas, bonitos,~ 1750100101   Sarda sarda  
##  3 Albania Barracu~ 37              Miscellaneous p~ 17710001XX   Sphyraena spp
##  4 Albania Blue an~ 45              Shrimps, prawns  2280203101   Aristeus ant~
##  5 Albania Blue wh~ 32              Cods, hakes, ha~ 1480403301   Micromesisti~
##  6 Albania Bluefish 37              Miscellaneous p~ 1702021301   Pomatomus sa~
##  7 Albania Bogue    33              Miscellaneous c~ 1703926101   Boops boops  
##  8 Albania Caramot~ 45              Shrimps, prawns  2280100117   Penaeus kera~
##  9 Albania Catshar~ 38              Sharks, rays, c~ 10801003XX   Scyliorhinus~
## 10 Albania Common ~ 57              Squids, cuttlef~ 3210200202   Sepia offici~
## # ... with 17,682 more rows, and 65 more variables: `FAO major fishing
## #   area` <fct>, Measure <fct>, `1950` <dbl>, `1951` <dbl>, `1952` <dbl>,
## #   `1953` <dbl>, `1954` <dbl>, `1955` <dbl>, `1956` <dbl>, `1957` <dbl>,
## #   `1958` <dbl>, `1959` <dbl>, `1960` <dbl>, `1961` <dbl>, `1962` <dbl>,
## #   `1963` <dbl>, `1964` <dbl>, `1965` <dbl>, `1966` <dbl>, `1967` <dbl>,
## #   `1968` <dbl>, `1969` <dbl>, `1970` <dbl>, `1971` <dbl>, `1972` <dbl>,
## #   `1973` <dbl>, `1974` <dbl>, `1975` <dbl>, `1976` <dbl>, `1977` <dbl>,
## #   `1978` <dbl>, `1979` <dbl>, `1980` <dbl>, `1981` <dbl>, `1982` <dbl>,
## #   `1983` <dbl>, `1984` <dbl>, `1985` <dbl>, `1986` <dbl>, `1987` <dbl>,
## #   `1988` <dbl>, `1989` <dbl>, `1990` <dbl>, `1991` <dbl>, `1992` <dbl>,
## #   `1993` <dbl>, `1994` <dbl>, `1995` <dbl>, `1996` <dbl>, `1997` <dbl>,
## #   `1998` <dbl>, `1999` <dbl>, `2000` <dbl>, `2001` <dbl>, `2002` <dbl>,
## #   `2003` <dbl>, `2004` <dbl>, `2005` <dbl>, `2006` <dbl>, `2007` <dbl>,
## #   `2008` <dbl>, `2009` <dbl>, `2010` <dbl>, `2011` <dbl>, `2012` <dbl>
```


8. Are these data tidy? Why or why not, and, how do you know? Use the appropriate pivot function to tidy the data. Remove the NA's. Put the tidy data frame into a new object `fisheries_tidy`.  
+ These data are not tidy! Look at all those columns as years, which should just be another variable.

```r
fisheries_tidy <- fisheries %>%
  pivot_longer('1950':'2012',
               names_to = "year",
               values_to = "catch",
               values_drop_na = TRUE
               )
fisheries_tidy
```

```
## # A tibble: 357,807 x 10
##    country commname ISSCAAP_spgroup ISSCAAP_spgroup~ ASFIS_spcode ASFIS_sciname
##    <fct>   <fct>    <fct>           <fct>            <fct>        <fct>        
##  1 Albania Angelsh~ 38              Sharks, rays, c~ 10903XXXXX   Squatinidae  
##  2 Albania Angelsh~ 38              Sharks, rays, c~ 10903XXXXX   Squatinidae  
##  3 Albania Angelsh~ 38              Sharks, rays, c~ 10903XXXXX   Squatinidae  
##  4 Albania Angelsh~ 38              Sharks, rays, c~ 10903XXXXX   Squatinidae  
##  5 Albania Angelsh~ 38              Sharks, rays, c~ 10903XXXXX   Squatinidae  
##  6 Albania Angelsh~ 38              Sharks, rays, c~ 10903XXXXX   Squatinidae  
##  7 Albania Angelsh~ 38              Sharks, rays, c~ 10903XXXXX   Squatinidae  
##  8 Albania Angelsh~ 38              Sharks, rays, c~ 10903XXXXX   Squatinidae  
##  9 Albania Angelsh~ 38              Sharks, rays, c~ 10903XXXXX   Squatinidae  
## 10 Albania Angelsh~ 38              Sharks, rays, c~ 10903XXXXX   Squatinidae  
## # ... with 357,797 more rows, and 4 more variables: `FAO major fishing
## #   area` <fct>, Measure <fct>, year <chr>, catch <dbl>
```



9. Refocus the data only to include country, ISSCAAP_spgroupname, ASFIS_spcode, ASFIS_sciname, year, and catch.

```r
fisheries_tidy2 <- select(fisheries_tidy, country, ISSCAAP_spgroupname, ASFIS_spcode, ASFIS_sciname, year, catch)
fisheries_tidy2
```

```
## # A tibble: 357,807 x 6
##    country ISSCAAP_spgroupname     ASFIS_spcode ASFIS_sciname year  catch
##    <fct>   <fct>                   <fct>        <fct>         <chr> <dbl>
##  1 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   1996     53
##  2 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   1997     20
##  3 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   1998     31
##  4 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   1999     30
##  5 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   2000     30
##  6 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   2001     16
##  7 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   2002     79
##  8 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   2003      1
##  9 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   2004      4
## 10 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   2005     68
## # ... with 357,797 more rows
```


10. Re-check the classes of `fisheries_tidy2`. Notice that "catch" is shown as a character! This is a problem because we will want to treat it as a numeric. How will you deal with this?

```r
fisheries_tidy2 <- fisheries_tidy2 %>%
  mutate_at("catch", as.numeric)
fisheries_tidy2
```

```
## # A tibble: 357,807 x 6
##    country ISSCAAP_spgroupname     ASFIS_spcode ASFIS_sciname year  catch
##    <fct>   <fct>                   <fct>        <fct>         <chr> <dbl>
##  1 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   1996     53
##  2 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   1997     20
##  3 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   1998     31
##  4 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   1999     30
##  5 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   2000     30
##  6 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   2001     16
##  7 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   2002     79
##  8 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   2003      1
##  9 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   2004      4
## 10 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   2005     68
## # ... with 357,797 more rows
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
fisheries_tidy2 %>% filter(year == "2000") %>%
  group_by(country) %>%
  summarise(max_catch = max(catch)) %>%
  arrange(desc(max_catch)) %>%
  head(1)
```

```
## # A tibble: 1 x 2
##   country max_catch
##   <fct>       <dbl>
## 1 Peru      9575717
```

13. Which country caught the most sardines (_Sardina_) between the years 1990-2000?

```r
fisheries_tidy2 %>%
  filter(year >= 1990, year <= 2000) %>%
  filter(grepl('Sardina', ASFIS_sciname)) %>%
  group_by(country) %>%
  summarise(max_sardines = max(catch)) %>%
  arrange(desc(max_sardines)) %>%
  head(1)
```

```
## # A tibble: 1 x 2
##   country max_sardines
##   <fct>          <dbl>
## 1 Morocco       556152
```

14. Which five countries caught the most cephalopods between 2008-2012?

```r
levels(fisheries_tidy2$ISSCAAP_spgroupname)
```

```
##  [1] "Abalones, winkles, conchs"           
##  [2] "Carps, barbels and other cyprinids"  
##  [3] "Clams, cockles, arkshells"           
##  [4] "Cods, hakes, haddocks"               
##  [5] "Crabs, seaspiders"                   
##  [6] "Flounders, halibuts, soles"          
##  [7] "Herrings, sardines, anchovies"       
##  [8] "Horseshoe crabs and other arachnoids"
##  [9] "King crabs, squatlobsters"           
## [10] "Lobsters, spinyrock lobsters"        
## [11] "Marine fishes not identified"        
## [12] "Miscellaneous aquatic invertebrates" 
## [13] "Miscellaneous coastal fishes"        
## [14] "Miscellaneous demersal fishes"       
## [15] "Miscellaneous diadromous fishes"     
## [16] "Miscellaneous marine crustaceans"    
## [17] "Miscellaneous marine molluscs"       
## [18] "Miscellaneous pelagic fishes"        
## [19] "Mussels"                             
## [20] "Oysters"                             
## [21] "Salmons, trouts, smelts"             
## [22] "Scallops, pectens"                   
## [23] "Seaurchins and other echinoderms"    
## [24] "Shads"                               
## [25] "Sharks, rays, chimaeras"             
## [26] "Shrimps, prawns"                     
## [27] "Squids, cuttlefishes, octopuses"     
## [28] "Sturgeons, paddlefishes"             
## [29] "Tilapias and other cichlids"         
## [30] "Tunas, bonitos, billfishes"
```



```r
fisheries_tidy2 %>% 
  filter(grepl('Squids', ISSCAAP_spgroupname)) %>% 
  filter(year <= 2012 & year >= 2008) %>% 
  group_by(country) %>% 
  summarise(catch = sum(catch)) %>% 
  arrange(desc(catch)) %>%
  head(5)
```

```
## # A tibble: 5 x 2
##   country              catch
##   <fct>                <dbl>
## 1 China              4785139
## 2 Peru               2274232
## 3 Japan              1644085
## 4 Korea, Republic of 1535454
## 5 Viet Nam           1292000
```


15. Given the top five countries from question (14) above, which species was the highest catch total? The lowest?

```r
ceph_catch <- 
  fisheries_tidy2 %>% 
  filter(grepl('Squids', ISSCAAP_spgroupname)) %>% 
  filter(year>=2008 & year<=2012) %>% 
  group_by(ASFIS_sciname) %>% 
  summarize(catch_total=sum(catch, na.rm=T)) %>% 
  arrange((catch_total))
```


```r
first(ceph_catch$ASFIS_sciname)
```

```
## [1] Todarodes filippovae
## 1548 Levels: Ablennes hians Abramis brama ... Zygochlamys patagonica
```


```r
last(ceph_catch$ASFIS_sciname)
```

```
## [1] Dosidicus gigas
## 1548 Levels: Ablennes hians Abramis brama ... Zygochlamys patagonica
```

16. In some cases, the taxonomy of the fish being caught is unclear. Make a new data frame called `coastal_fish` that shows the taxonomic composition of "Miscellaneous coastal fishes" within the ISSCAAP_spgroupname column.

```r
coastal_fish <-
  fisheries_tidy2 %>%
  filter(ISSCAAP_spgroupname == "Miscellaneous coastal fishes")
levels(coastal_fish$ASFIS_sciname)
```

```
##    [1] "Ablennes hians"                   "Abramis brama"                   
##    [3] "Abramis spp"                      "Acanthistius brasilianus"        
##    [5] "Acanthocybium solandri"           "Acanthopagrus berda"             
##    [7] "Acanthopagrus bifasciatus"        "Acanthopagrus latus"             
##    [9] "Acanthopagrus schlegeli"          "Acanthuridae"                    
##   [11] "Acanthurus sohal"                 "Acetes erythraeus"               
##   [13] "Acetes japonicus"                 "Acipenser gueldenstaedtii"       
##   [15] "Acipenser medirostris"            "Acipenser ruthenus"              
##   [17] "Acipenser stellatus"              "Acipenser transmontanus"         
##   [19] "Acipenseridae"                    "Aequipecten opercularis"         
##   [21] "Aethaloperca rogaa"               "Albula vulpes"                   
##   [23] "Alectis alexandrinus"             "Alepes djedaba"                  
##   [25] "Alepisaurus ferox"                "Alepocephalus bairdii"           
##   [27] "Alepocephalus spp"                "Allocyttus niger"                
##   [29] "Allocyttus verrucosus"            "Allothunnus fallai"              
##   [31] "Alopias pelagicus"                "Alopias spp"                     
##   [33] "Alopias superciliosus"            "Alopias vulpinus"                
##   [35] "Alosa aestivalis"                 "Alosa alosa"                     
##   [37] "Alosa fallax"                     "Alosa mediocris"                 
##   [39] "Alosa pontica"                    "Alosa pseudoharengus"            
##   [41] "Alosa sapidissima"                "Alosa spp"                       
##   [43] "Ambassidae"                       "Amblygaster sirm"                
##   [45] "Ammodytes personatus"             "Ammodytes spp"                   
##   [47] "Amphichthys cryptocentrus"        "Anadara granosa"                 
##   [49] "Anadara ovalis"                   "Anadara spp"                     
##   [51] "Anarhichas denticulatus"          "Anarhichas lupus"                
##   [53] "Anarhichas minor"                 "Anarhichas spp"                  
##   [55] "Anchoa hepsetus"                  "Anchoa marinii"                  
##   [57] "Anchoa nasus"                     "Anodontostoma chacunda"          
##   [59] "Anoplopoma fimbria"               "Antimora rostrata"               
##   [61] "Aphanopus carbo"                  "Aphanopus intermedius"           
##   [63] "Aphareus rutilans"                "Aphia minuta"                    
##   [65] "Aplodactylus punctatus"           "Apogonidae"                      
##   [67] "Aprion virescens"                 "Apsilus fuscus"                  
##   [69] "Arca noae"                        "Arca spp"                        
##   [71] "Arca zebra"                       "Archosargus probatocephalus"     
##   [73] "Archosargus rhomboidalis"         "Arctica islandica"               
##   [75] "Arctoscopus japonicus"            "Argentina silus"                 
##   [77] "Argentina sphyraena"              "Argentina spp"                   
##   [79] "Argopecten gibbus"                "Argopecten irradians"            
##   [81] "Argopecten purpuratus"            "Argopecten ventricosus"          
##   [83] "Argyrops spinifer"                "Argyrosomus hololepidotus"       
##   [85] "Argyrosomus regius"               "Argyrozona argyrozona"           
##   [87] "Ariidae"                          "Ariomma indica"                  
##   [89] "Aristaeomorpha foliacea"          "Aristeidae"                      
##   [91] "Aristeus antennatus"              "Aristeus spp"                    
##   [93] "Aristeus varidens"                "Arius thalassinus"               
##   [95] "Arripis georgianus"               "Arripis trutta"                  
##   [97] "Artemesia longinaris"             "Artemia salina"                  
##   [99] "Aspitrigla cuculus"               "Aspius aspius"                   
##  [101] "Asterias rubens"                  "Asteroidea"                      
##  [103] "Atheresthes evermanni"            "Atheresthes stomias"             
##  [105] "Atherina boyeri"                  "Atherina hepsetus"               
##  [107] "Atherinidae"                      "Atractoscion aequidens"          
##  [109] "Atractoscion nobilis"             "Atrobucca nibe"                  
##  [111] "Atule mate"                       "Aulacomya ater"                  
##  [113] "Austroglossus microlepis"         "Austroglossus pectoralis"        
##  [115] "Austroglossus spp"                "Austromegabalanus psittacus"     
##  [117] "Auxis rochei"                     "Auxis thazard"                   
##  [119] "Auxis thazard, A. rochei"         "Babylonia spirata"               
##  [121] "Balistes carolinensis"            "Balistidae"                      
##  [123] "Barbourisia rufa"                 "Bathyraja brachyurops"           
##  [125] "Bathyraja eatonii"                "Bathyraja irrasa"                
##  [127] "Bathyraja maccaini"               "Bathyraja macloviana"            
##  [129] "Bathyraja meridionalis"           "Bathyraja murrayi"               
##  [131] "Bathyraja spp"                    "Batrachoididae"                  
##  [133] "Belone belone"                    "Belonidae"                       
##  [135] "Benthodesmus spp"                 "Benthosema pterotum"             
##  [137] "Berryteuthis magister"            "Beryx decadactylus"              
##  [139] "Beryx splendens"                  "Beryx spp"                       
##  [141] "Bivalvia"                         "Blicca bjoerkna"                 
##  [143] "Bolbometopon muricatum"           "Boops boops"                     
##  [145] "Boreogadus saida"                 "Borostomias antarcticus"         
##  [147] "Bothidae"                         "Bothus pantherinus"              
##  [149] "Brachydeuterus auritus"           "Brachyura"                       
##  [151] "Brama australis"                  "Brama brama"                     
##  [153] "Bramidae"                         "Branchiostegidae"                
##  [155] "Bregmaceros mcclellandi"          "Brevoortia aurea"                
##  [157] "Brevoortia patronus"              "Brevoortia pectinata"            
##  [159] "Brevoortia tyrannus"              "Brosme brosme"                   
##  [161] "Brotula barbata"                  "Buccinum undatum"                
##  [163] "Busycon spp"                      "Caesionidae"                     
##  [165] "Calamus spp"                      "Calanus finmarchicus"            
##  [167] "Callianassa spp"                  "Callinectes danae"               
##  [169] "Callinectes sapidus"              "Callista chione"                 
##  [171] "Callorhinchidae"                  "Callorhinchus callorynchus"      
##  [173] "Callorhinchus capensis"           "Callorhinchus milii"             
##  [175] "Campogramma glaycos"              "Cancer borealis"                 
##  [177] "Cancer edwardsii"                 "Cancer irroratus"                
##  [179] "Cancer magister"                  "Cancer pagurus"                  
##  [181] "Cancer productus"                 "Cantherhines (=Navodon) spp"     
##  [183] "Caprodon longimanus"              "Caproidae"                       
##  [185] "Capromimus abbreviatus"           "Capros aper"                     
##  [187] "Carangidae"                       "Carangoides bajad"               
##  [189] "Carangoides fulvoguttatus"        "Carangoides malabaricus"         
##  [191] "Caranx crysos"                    "Caranx hippos"                   
##  [193] "Caranx ignobilis"                 "Caranx melampygus"               
##  [195] "Caranx rhonchus"                  "Caranx ruber"                    
##  [197] "Caranx sexfasciatus"              "Caranx spp"                      
##  [199] "Carassius auratus"                "Carassius carassius"             
##  [201] "Carcharhinidae"                   "Carcharhinus acronotus"          
##  [203] "Carcharhinus brachyurus"          "Carcharhinus brevipinna"         
##  [205] "Carcharhinus falciformis"         "Carcharhinus isodon"             
##  [207] "Carcharhinus leucas"              "Carcharhinus limbatus"           
##  [209] "Carcharhinus longimanus"          "Carcharhinus obscurus"           
##  [211] "Carcharhinus plumbeus"            "Carcharhinus porosus"            
##  [213] "Carcharhinus sorrah"              "Carcharias taurus"               
##  [215] "Carcharodon carcharias"           "Carcinus aestuarii"              
##  [217] "Carcinus maenas"                  "Cardiidae"                       
##  [219] "Carpilius corallinus"             "Caulolatilus chrysops"           
##  [221] "Caulolatilus microps"             "Caulolatilus princeps"           
##  [223] "Centriscops humerosus"            "Centroberyx affinis"             
##  [225] "Centrolabrus exoletus"            "Centrolophidae"                  
##  [227] "Centrolophus niger"               "Centrophorus granulosus"         
##  [229] "Centrophorus lusitanicus"         "Centrophorus squamosus"          
##  [231] "Centropomus spp"                  "Centropomus undecimalis"         
##  [233] "Centropristis striata"            "Centroscyllium fabricii"         
##  [235] "Centroscymnus coelolepis"         "Centroscymnus crepidater"        
##  [237] "Cephalopholis argus"              "Cephalopholis boenak"            
##  [239] "Cephalopholis fulva"              "Cephalopholis hemistiktos"       
##  [241] "Cephalopholis miniata"            "Cephalopoda"                     
##  [243] "Cephaloscyllium isabellum"        "Cepola macrophthalma"            
##  [245] "Cerastoderma edule"               "Cervimunida johni"               
##  [247] "Cetengraulis edentulus"           "Cetengraulis mysticetus"         
##  [249] "Cetorhinus maximus"               "Chaceon affinis"                 
##  [251] "Chaceon fenneri"                  "Chaceon maritae"                 
##  [253] "Chaceon notialis"                 "Chaceon quinquedens"             
##  [255] "Chaceon spp"                      "Chaenocephalus aceratus"         
##  [257] "Chaenodraco wilsoni"              "Chaetodipterus zonatus"          
##  [259] "Chamelea gallina"                 "Champsocephalus esox"            
##  [261] "Champsocephalus gunnari"          "Channichthyidae"                 
##  [263] "Channichthys rhinoceratus"        "Chanos chanos"                   
##  [265] "Charybdis spp"                    "Cheilinus undulatus"             
##  [267] "Cheilodactylus bergi"             "Cheilodactylus variegatus"       
##  [269] "Cheimerius nufar"                 "Chelidonichthys capensis"        
##  [271] "Chelidonichthys kumu"             "Chelidonichthys lastoviza"       
##  [273] "Chelidonichthys lucerna"          "Chelon haematocheilus"           
##  [275] "Chelon labrosus"                  "Chimaera monstrosa"              
##  [277] "Chimaera phantasma"               "Chimaeriformes"                  
##  [279] "Chione stutchburyi"               "Chionobathyscus dewitti"         
##  [281] "Chionodraco hamatus"              "Chionodraco myersi"              
##  [283] "Chionodraco rastrospinosus"       "Chionoecetes japonicus"          
##  [285] "Chionoecetes opilio"              "Chionoecetes spp"                
##  [287] "Chirocentrus dorab"               "Chirocentrus nudus"              
##  [289] "Chirocentrus spp"                 "Chlamys islandica"               
##  [291] "Chlorophthalmidae"                "Chloroscombrus chrysurus"        
##  [293] "Chloroscombrus orqueta"           "Choromytilus chorus"             
##  [295] "Chrysoblephus spp"                "Cilus gilberti"                  
##  [297] "Cirrhinus molitorella"            "Citharichthys sordidus"          
##  [299] "Citharidae"                       "Clepticus parrae"                
##  [301] "Clinocardium nuttallii"           "Clupanodon thrissa"              
##  [303] "Clupea harengus"                  "Clupea pallasii"                 
##  [305] "Clupeoidei"                       "Clupeonella cultriventris"       
##  [307] "Coelorinchus chilensis"           "Cololabis saira"                 
##  [309] "Concholepas concholepas"          "Conger conger"                   
##  [311] "Conger myriaster"                 "Conger oceanicus"                
##  [313] "Conger orbignyanus"               "Congridae"                       
##  [315] "Conodon nobilis"                  "Coregonus albula"                
##  [317] "Coregonus lavaretus"              "Coregonus spp"                   
##  [319] "Coris julis"                      "Coryphaena hippurus"             
##  [321] "Coryphaenoides rupestris"         "Coryphaenoides spp"              
##  [323] "Cottidae"                         "Cottoperca gobio"                
##  [325] "Crangon crangon"                  "Crangonidae"                     
##  [327] "Crassostrea gigas"                "Crassostrea iredalei"            
##  [329] "Crassostrea rhizophorae"          "Crassostrea spp"                 
##  [331] "Crassostrea virginica"            "Crenidens crenidens"             
##  [333] "Cromileptes altivelis"            "Crustacea"                       
##  [335] "Ctenolabrus rupestris"            "Cubiceps capensis"               
##  [337] "Cyclopterus lumpus"               "Cymatoceps nasutus"              
##  [339] "Cymbium cymbium"                  "Cymbium spp"                     
##  [341] "Cynoglossidae"                    "Cynomacrurus piriei"             
##  [343] "Cynoponticus coniceps"            "Cynoscion acoupa"                
##  [345] "Cynoscion analis"                 "Cynoscion arenarius"             
##  [347] "Cynoscion guatucupa"              "Cynoscion jamaicensis"           
##  [349] "Cynoscion leiarchus"              "Cynoscion nebulosus"             
##  [351] "Cynoscion regalis"                "Cynoscion spp"                   
##  [353] "Cynoscion striatus"               "Cynoscion virescens"             
##  [355] "Cyprinidae"                       "Cyprinus carpio"                 
##  [357] "Cypselurus agoo"                  "Cyttus novaezealandiae"          
##  [359] "Cyttus traversi"                  "Dactylopterus volitans"          
##  [361] "Dalatias licha"                   "Dasyatidae"                      
##  [363] "Dasyatis akajei"                  "Dasyatis americana"              
##  [365] "Dasyatis longa"                   "Dasyatis pastinaca"              
##  [367] "Dasyatis spp"                     "Dasyatis violacea"               
##  [369] "Deania calcea"                    "Deania profundorum"              
##  [371] "Decapterus macrosoma"             "Decapterus maruadsi"             
##  [373] "Decapterus russelli"              "Decapterus spp"                  
##  [375] "Dentex angolensis"                "Dentex congoensis"               
##  [377] "Dentex dentex"                    "Dentex macrophthalmus"           
##  [379] "Dentex spp"                       "Diagramma pictum"                
##  [381] "Diapterus auratus"                "Diastobranchus capensis"         
##  [383] "Dicentrarchus labrax"             "Dicentrarchus punctatus"         
##  [385] "Dicentrarchus spp"                "Dicologlossa cuneata"            
##  [387] "Diplodus annularis"               "Diplodus argenteus"              
##  [389] "Diplodus puntazzo"                "Diplodus sargus"                 
##  [391] "Diplodus spp"                     "Diplodus vulgaris"               
##  [393] "Dipturus chilensis"               "Dipturus innominatus"            
##  [395] "Dissostichus eleginoides"         "Dissostichus mawsoni"            
##  [397] "Donax spp"                        "Dorosoma cepedianum"             
##  [399] "Dosidicus gigas"                  "Drepane africana"                
##  [401] "Drepane punctata"                 "Dussumieria acuta"               
##  [403] "Dussumieria elopsoides"           "Echeneidae"                      
##  [405] "Echeneis naucrates"               "Echinodermata"                   
##  [407] "Echinoidea"                       "Echinorhinus brucus"             
##  [409] "Echinus esculentus"               "Elagatis bipinnulata"            
##  [411] "Elasmobranchii"                   "Electrona carlsbergi"            
##  [413] "Eledone cirrhosa"                 "Eledone moschata"                
##  [415] "Eledone spp"                      "Eleginops maclovinus"            
##  [417] "Eleginus gracilis"                "Eleginus navaga"                 
##  [419] "Eleutheronema tetradactylum"      "Elops lacerta"                   
##  [421] "Elops saurus"                     "Emmelichthyidae"                 
##  [423] "Emmelichthys nitidus"             "Enchelyopus cimbrius"            
##  [425] "Encrasicholina punctifer"         "Engraulidae"                     
##  [427] "Engraulis anchoita"               "Engraulis capensis"              
##  [429] "Engraulis encrasicolus"           "Engraulis japonicus"             
##  [431] "Engraulis mordax"                 "Engraulis ringens"               
##  [433] "Ensis directus"                   "Ensis ensis"                     
##  [435] "Ensis siliqua"                    "Eopsetta jordani"                
##  [437] "Ephippidae"                       "Epigonus spp"                    
##  [439] "Epigonus telescopus"              "Epinephelus adscensionis"        
##  [441] "Epinephelus aeneus"               "Epinephelus analogus"            
##  [443] "Epinephelus areolatus"            "Epinephelus caeruleopunctatus"   
##  [445] "Epinephelus caninus"              "Epinephelus chlorostigma"        
##  [447] "Epinephelus coioides"             "Epinephelus drummondhayi"        
##  [449] "Epinephelus fasciatus"            "Epinephelus flavolimbatus"       
##  [451] "Epinephelus fuscoguttatus"        "Epinephelus goreensis"           
##  [453] "Epinephelus guttatus"             "Epinephelus marginatus"          
##  [455] "Epinephelus merra"                "Epinephelus morio"               
##  [457] "Epinephelus morrhua"              "Epinephelus multinotatus"        
##  [459] "Epinephelus mystacinus"           "Epinephelus nigritus"            
##  [461] "Epinephelus niveatus"             "Epinephelus polylepis"           
##  [463] "Epinephelus polyphekadion"        "Epinephelus spp"                 
##  [465] "Epinephelus striatus"             "Epinephelus summana"             
##  [467] "Epinephelus tauvina"              "Eptatretus cirrhatus"            
##  [469] "Erilepis zonifer"                 "Erimacrus isenbeckii"            
##  [471] "Erugosquilla massavensis"         "Etelis oculatus"                 
##  [473] "Ethmalosa fimbriata"              "Ethmidium maculatum"             
##  [475] "Etmopterus princeps"              "Etmopterus spinax"               
##  [477] "Etmopterus spp"                   "Etrumeus teres"                  
##  [479] "Etrumeus whiteheadi"              "Eucinostomus melanopterus"       
##  [481] "Euthynnus affinis"                "Euthynnus alletteratus"          
##  [483] "Euthynnus lineatus"               "Eutrigla gurnardus"              
##  [485] "Exocoetidae"                      "Fistularia commersonii"          
##  [487] "Fistularia corneta"               "Fistularia tabacaria"            
##  [489] "Gadiculus argenteus"              "Gadiformes"                      
##  [491] "Gadus macrocephalus"              "Gadus morhua"                    
##  [493] "Gadus ogac"                       "Gaidropsarus ensis"              
##  [495] "Gaidropsarus spp"                 "Galatheidae"                     
##  [497] "Galeichthys feliceps"             "Galeocerdo cuvier"               
##  [499] "Galeoides decadactylus"           "Galeorhinus galeus"              
##  [501] "Galeus melastomus"                "Galeus murinus"                  
##  [503] "Gasterochisma melampus"           "Gasterosteus aculeatus"          
##  [505] "Gastropoda"                       "Gempylidae"                      
##  [507] "Genyonemus lineatus"              "Genypterus blacodes"             
##  [509] "Genypterus capensis"              "Genypterus chilensis"            
##  [511] "Genypterus maculatus"             "Genypterus spp"                  
##  [513] "Gerreidae"                        "Gerres nigri"                    
##  [515] "Gerres oblongus"                  "Gerres oyena"                    
##  [517] "Gerres spp"                       "Geryon longipes"                 
##  [519] "Ginglymostoma cirratum"           "Girella nigricans"               
##  [521] "Girella tricuspidata"             "Glossanodon semifasciatus"       
##  [523] "Glycymeris glycymeris"            "Glyptocephalus cynoglossus"      
##  [525] "Glyptocephalus zachirus"          "Gnathanodon speciosus"           
##  [527] "Gobiidae"                         "Gollum attenuatus"               
##  [529] "Gonatidae"                        "Grammoplites suppositus"         
##  [531] "Gymnocranius spp"                 "Gymnosarda unicolor"             
##  [533] "Gymnoscopelus nicholsi"           "Gymnura altavela"                
##  [535] "Gymnura marmorata"                "Haemulidae (=Pomadasyidae)"      
##  [537] "Haemulon album"                   "Haemulon plumierii"              
##  [539] "Haemulon spp"                     "Halaelurus canescens"            
##  [541] "Haliotis gigantea"                "Haliotis midae"                  
##  [543] "Haliotis rubra"                   "Haliotis spp"                    
##  [545] "Haliotis tuberculata"             "Haliporoides diomedeae"          
##  [547] "Haliporoides sibogae"             "Haliporoides triarthrus"         
##  [549] "Halobatrachus didactylus"         "Harengula spp"                   
##  [551] "Harengula thrissina"              "Harpadon nehereus"               
##  [553] "Helicolenus dactylopterus"        "Hemiramphus balao"               
##  [555] "Hemiramphus brasiliensis"         "Hemiramphus spp"                 
##  [557] "Hemitriakis japanica"             "Heptranchias perlo"              
##  [559] "Herklotsichthys quadrimaculat."   "Heterocarpus reedi"              
##  [561] "Heterocarpus vicarius"            "Hexagrammos decagrammus"         
##  [563] "Hexanchus griseus"                "Himantura gerrardi"              
##  [565] "Hippoglossoides elassodon"        "Hippoglossoides platessoides"    
##  [567] "Hippoglossus hippoglossus"        "Hippoglossus stenolepis"         
##  [569] "Holocentridae"                    "Holothuria fuscogilva"           
##  [571] "Holothuria nobilis"               "Holothuria scabra"               
##  [573] "Holothuroidea"                    "Homalaspis plana"                
##  [575] "Homarus americanus"               "Homarus gammarus"                
##  [577] "Hoplopagrus guentherii"           "Hoplostethus atlanticus"         
##  [579] "Hoplostethus mediterraneus"       "Huso huso"                       
##  [581] "Hydrolagus colliei"               "Hydrolagus novaezealandiae"      
##  [583] "Hydrolagus spp"                   "Hyperoglyphe antarctica"         
##  [585] "Hyperoglyphe bythites"            "Hyperoglyphe perciformis"        
##  [587] "Hypomesus pretiosus"              "Hypophthalmichthys molitrix"     
##  [589] "Hypoptychus dybowskii"            "Hyporhamphus sajori"             
##  [591] "Ibacus ciliatus"                  "Ilisha africana"                 
##  [593] "Ilisha elongata"                  "Illex argentinus"                
##  [595] "Illex coindetii"                  "Illex illecebrosus"              
##  [597] "Invertebrata"                     "Isacia conceptionis"             
##  [599] "Isopisthus parvipinnis"           "Istiophoridae"                   
##  [601] "Istiophorus albicans"             "Istiophorus platypterus"         
##  [603] "Isurus oxyrinchus"                "Isurus paucus"                   
##  [605] "Isurus spp"                       "Jasus edwardsii"                 
##  [607] "Jasus frontalis"                  "Jasus lalandii"                  
##  [609] "Jasus novaehollandiae"            "Jasus paulensis"                 
##  [611] "Jasus tristani"                   "Jasus verreauxi"                 
##  [613] "Joturus pichardi"                 "Kathetostoma giganteum"          
##  [615] "Katsuwonus pelamis"               "Konosirus punctatus"             
##  [617] "Kyphosidae"                       "Labridae"                        
##  [619] "Labrus bergylta"                  "Labrus merula"                   
##  [621] "Lachnolaimus maximus"             "Lactarius lactarius"             
##  [623] "Laemonema longipes"               "Lagocephalus sceleratus"         
##  [625] "Lagodon rhomboides"               "Lamna nasus"                     
##  [627] "Lamnidae"                         "Lampanyctodes hectoris"          
##  [629] "Lampanyctus achirus"              "Lampetra fluviatilis"            
##  [631] "Lampris guttatus"                 "Lampris immaculatus"             
##  [633] "Larimichthys croceus"             "Larimichthys polyactis"          
##  [635] "Larimus breviceps"                "Lateolabrax japonicus"           
##  [637] "Lates calcarifer"                 "Latridae"                        
##  [639] "Leiognathidae"                    "Leiognathus spp"                 
##  [641] "Leiostomus xanthurus"             "Lepas spp"                       
##  [643] "Lepidocybium flavobrunneum"       "Lepidoperca pulchella"           
##  [645] "Lepidopsetta bilineata"           "Lepidopus caudatus"              
##  [647] "Lepidorhombus boscii"             "Lepidorhombus spp"               
##  [649] "Lepidorhombus whiffiagonis"       "Lepidorhynchus denticulatus"     
##  [651] "Lepidotrigla brachyoptera"        "Leptocharias smithii"            
##  [653] "Leptomelanosoma indicum"          "Lethrinidae"                     
##  [655] "Lethrinus atlanticus"             "Lethrinus borbonicus"            
##  [657] "Lethrinus harak"                  "Lethrinus lentjan"               
##  [659] "Lethrinus mahsena"                "Lethrinus microdon"              
##  [661] "Lethrinus miniatus"               "Lethrinus nebulosus"             
##  [663] "Lethrinus obsoletus"              "Lethrinus xanthochilus"          
##  [665] "Leuciscus idus"                   "Libinia emarginata"              
##  [667] "Lichia amia"                      "Lile stolifera"                  
##  [669] "Limanda aspera"                   "Limanda ferruginea"              
##  [671] "Limanda limanda"                  "Limulus polyphemus"              
##  [673] "Lithodes aequispina"              "Lithodes murrayi"                
##  [675] "Lithodes santolla"                "Lithodes spp"                    
##  [677] "Lithodidae"                       "Lithognathus lithognathus"       
##  [679] "Lithognathus mormyrus"            "Lithognathus spp"                
##  [681] "Littorina littorea"               "Littorina spp"                   
##  [683] "Liza aurata"                      "Liza klunzingeri"                
##  [685] "Liza saliens"                     "Lobotes pacificus"               
##  [687] "Lobotes surinamensis"             "Loliginidae, Ommastrephidae"     
##  [689] "Loligo duvauceli"                 "Loligo forbesi"                  
##  [691] "Loligo gahi"                      "Loligo opalescens"               
##  [693] "Loligo pealeii"                   "Loligo reynaudii"                
##  [695] "Loligo spp"                       "Loligo vulgaris"                 
##  [697] "Lophiidae"                        "Lophius americanus"              
##  [699] "Lophius budegassa"                "Lophius gastrophysus"            
##  [701] "Lophius piscatorius"              "Lophius spp"                     
##  [703] "Lophius vaillanti"                "Lophius vomerinus"               
##  [705] "Lopholatilus chamaeleonticeps"    "Loxechinus albus"                
##  [707] "Lutjanidae"                       "Lutjanus analis"                 
##  [709] "Lutjanus argentimaculatus"        "Lutjanus argentiventris"         
##  [711] "Lutjanus bohar"                   "Lutjanus buccanella"             
##  [713] "Lutjanus campechanus"             "Lutjanus cyanopterus"            
##  [715] "Lutjanus gibbus"                  "Lutjanus griseus"                
##  [717] "Lutjanus guttatus"                "Lutjanus johnii"                 
##  [719] "Lutjanus kasmira"                 "Lutjanus malabaricus"            
##  [721] "Lutjanus peru"                    "Lutjanus purpureus"              
##  [723] "Lutjanus quinquelineatus"         "Lutjanus spp"                    
##  [725] "Lutjanus synagris"                "Lutjanus vitta"                  
##  [727] "Lutjanus vivanus"                 "Lycodes spp"                     
##  [729] "Macrodon ancylodon"               "Macroramphosus scolopax"         
##  [731] "Macrouridae"                      "Macrourus berglax"               
##  [733] "Macrourus carinatus"              "Macrourus holotrachys"           
##  [735] "Macrourus spp"                    "Macrourus whitsoni"              
##  [737] "Macrozoarces americanus"          "Macruronus magellanicus"         
##  [739] "Macruronus novaezelandiae"        "Magnisudis atlantica"            
##  [741] "Maja squinado"                    "Makaira indica"                  
##  [743] "Makaira nigricans"                "Malacanthus plumieri"            
##  [745] "Mallotus villosus"                "Mancopsetta maculata"            
##  [747] "Manta birostris"                  "Martialia hyadesi"               
##  [749] "Maurolicus muelleri"              "Megalaspis cordyla"              
##  [751] "Megalops atlanticus"              "Megalops cyprinoides"            
##  [753] "Melanogrammus aeglefinus"         "Mene maculata"                   
##  [755] "Menidia menidia"                  "Menippe mercenaria"              
##  [757] "Menticirrhus americanus"          "Menticirrhus littoralis"         
##  [759] "Menticirrhus saxatilis"           "Menticirrhus spp"                
##  [761] "Mercenaria mercenaria"            "Meretrix lusoria"                
##  [763] "Meretrix spp"                     "Merlangius merlangus"            
##  [765] "Merluccius albidus"               "Merluccius angustimanus"         
##  [767] "Merluccius australis"             "Merluccius bilinearis"           
##  [769] "Merluccius capensis"              "Merluccius capensis, M.paradoxus"
##  [771] "Merluccius gayi"                  "Merluccius hubbsi"               
##  [773] "Merluccius merluccius"            "Merluccius polli"                
##  [775] "Merluccius productus"             "Merluccius senegalensis"         
##  [777] "Merluccius spp"                   "Mesodesma donacium"              
##  [779] "Mesogobius batrachocephalus"      "Metanephrops andamanicus"        
##  [781] "Metanephrops challengeri"         "Metanephrops mozambicus"         
##  [783] "Metanephrops spp"                 "Metapenaeus endeavouri"          
##  [785] "Metapenaeus joyneri"              "Metapenaeus monoceros"           
##  [787] "Metapenaeus spp"                  "Microchirus spp"                 
##  [789] "Microgadus proximus"              "Microgadus tomcod"               
##  [791] "Micromesistius australis"         "Micromesistius poutassou"        
##  [793] "Micropogonias furnieri"           "Micropogonias spp"               
##  [795] "Micropogonias undulatus"          "Microstomus kitt"                
##  [797] "Microstomus pacificus"            "Miichthys miiuy"                 
##  [799] "Mithrax armatus"                  "Mobula mobular"                  
##  [801] "Mobulidae"                        "Modiolus spp"                    
##  [803] "Mola mola"                        "Mollusca"                        
##  [805] "Molva dypterygia"                 "Molva macrophthalma"             
##  [807] "Molva molva"                      "Molva spp"                       
##  [809] "Monacanthidae"                    "Monotaxis grandoculis"           
##  [811] "Mora moro"                        "Moridae"                         
##  [813] "Morone americana"                 "Morone saxatilis"                
##  [815] "Moroteuthis ingens"               "Moroteuthis robustus"            
##  [817] "Mugil cephalus"                   "Mugil curema"                    
##  [819] "Mugil incilis"                    "Mugil liza"                      
##  [821] "Mugil soiuy"                      "Mugilidae"                       
##  [823] "Mulinia spp"                      "Mullidae"                        
##  [825] "Mulloidichthys flavolineatus"     "Mullus argentinae"               
##  [827] "Mullus barbatus"                  "Mullus spp"                      
##  [829] "Mullus surmuletus"                "Munida gregaria"                 
##  [831] "Muraena helena"                   "Muraenesox cinereus"             
##  [833] "Muraenesox spp"                   "Muraenidae"                      
##  [835] "Muraenolepis microps"             "Muraenolepis spp"                
##  [837] "Murex spp"                        "Mustelus antarcticus"            
##  [839] "Mustelus asterias"                "Mustelus canis"                  
##  [841] "Mustelus henlei"                  "Mustelus lenticulatus"           
##  [843] "Mustelus mustelus"                "Mustelus schmitti"               
##  [845] "Mustelus spp"                     "Mya arenaria"                    
##  [847] "Mycteroperca bonaci"              "Mycteroperca microlepis"         
##  [849] "Mycteroperca phenax"              "Mycteroperca spp"                
##  [851] "Mycteroperca venenosa"            "Mycteroperca xenarcha"           
##  [853] "Myctophidae"                      "Myliobatidae"                    
##  [855] "Myliobatis aquila"                "Myoxocephalus scorpius"          
##  [857] "Myoxocephalus spp"                "Mytilidae"                       
##  [859] "Mytilus chilensis"                "Mytilus coruscus"                
##  [861] "Mytilus edulis"                   "Mytilus galloprovincialis"       
##  [863] "Mytilus planulatus"               "Mytilus platensis"               
##  [865] "Myxinidae"                        "Naso unicornis"                  
##  [867] "Natantia"                         "Naucrates ductor"                
##  [869] "Necora puber"                     "Negaprion brevirostris"          
##  [871] "Nemadactylus macropterus"         "Nemadactylus spp"                
##  [873] "Nematalosa nasus"                 "Nematopalaemon hastatus"         
##  [875] "Nematopalaemon schmitti"          "Nemipteridae"                    
##  [877] "Nemipterus japonicus"             "Nemipterus randalli"             
##  [879] "Nemipterus spp"                   "Nemipterus virgatus"             
##  [881] "Neocyttus rhomboidalis"           "Neopagetopsis ionah"             
##  [883] "Nephrops norvegicus"              "Nezumia aequalis"                
##  [885] "Nibea mitsukurii"                 "Normanichthys crockeri"          
##  [887] "Notolepis spp"                    "Notopogon lilliei"               
##  [889] "Notorynchus cepedianus"           "Notothenia acuta"                
##  [891] "Notothenia coriiceps"             "Notothenia gibberifrons"         
##  [893] "Notothenia kempi"                 "Notothenia neglecta"             
##  [895] "Notothenia rossii"                "Notothenia squamifrons"          
##  [897] "Nototheniidae"                    "Nototheniops larseni"            
##  [899] "Nototheniops mizops"              "Nototheniops nudifrons"          
##  [901] "Nototheniops nybelini"            "Nototodarus sloanii"             
##  [903] "Oblada melanura"                  "Octopodidae"                     
##  [905] "Octopus maya"                     "Octopus vulgaris"                
##  [907] "Ocyurus chrysurus"                "Odontesthes regia"               
##  [909] "Odontesthes smitti"               "Oligoplites refulgens"           
##  [911] "Ommastrephes bartrami"            "Oncorhynchus gorbuscha"          
##  [913] "Oncorhynchus keta"                "Oncorhynchus kisutch"            
##  [915] "Oncorhynchus masou"               "Oncorhynchus mykiss"             
##  [917] "Oncorhynchus nerka"               "Oncorhynchus spp"                
##  [919] "Oncorhynchus tshawytscha"         "Ophichthidae"                    
##  [921] "Ophidiidae"                       "Ophiodon elongatus"              
##  [923] "Opisthonema libertate"            "Opisthonema oglinum"             
##  [925] "Orcynopsis unicolor"              "Oreochromis (=Tilapia) spp"      
##  [927] "Oreosomatidae"                    "Orthopristis chrysoptera"        
##  [929] "Osmerus eperlanus"                "Osmerus mordax"                  
##  [931] "Osmerus spp, Hypomesus spp"       "Osteichthyes"                    
##  [933] "Ostraciidae"                      "Ostrea chilensis"                
##  [935] "Ostrea edulis"                    "Ostrea lutaria"                  
##  [937] "Ostreola conchaphila"             "Otolithes ruber"                 
##  [939] "Oxynotus centrina"                "Oxynotus paradoxus"              
##  [941] "Pagellus acarne"                  "Pagellus bellottii"              
##  [943] "Pagellus bogaraveo"               "Pagellus erythrinus"             
##  [945] "Pagellus spp"                     "Pagothenia hansoni"              
##  [947] "Pagrus auratus"                   "Pagrus caeruleostictus"          
##  [949] "Pagrus pagrus"                    "Pagrus spp"                      
##  [951] "Palaemon adspersus"               "Palaemon longirostris"           
##  [953] "Palaemon serratus"                "Palaemonidae"                    
##  [955] "Palinuridae"                      "Palinurus delagoae"              
##  [957] "Palinurus elephas"                "Palinurus gilchristi"            
##  [959] "Palinurus mauritanicus"           "Palinurus spp"                   
##  [961] "Pampus argenteus"                 "Pampus spp"                      
##  [963] "Pandalopsis japonica"             "Pandalus borealis"               
##  [965] "Pandalus goniurus"                "Pandalus hypsinotus"             
##  [967] "Pandalus jordani"                 "Pandalus kessleri"               
##  [969] "Pandalus montagui"                "Pandalus platyceros"             
##  [971] "Pandalus spp"                     "Panopea abrupta"                 
##  [973] "Panulirus argus"                  "Panulirus cygnus"                
##  [975] "Panulirus gracilis"               "Panulirus homarus"               
##  [977] "Panulirus longipes"               "Panulirus ornatus"               
##  [979] "Panulirus spp"                    "Paphia spp"                      
##  [981] "Paphies australis"                "Paracentrotus lividus"           
##  [983] "Parachaenichthys georgianus"      "Paragaleus pectoralis"           
##  [985] "Paralabrax humeralis"             "Paralabrax spp"                  
##  [987] "Paralichthys californicus"        "Paralichthys dentatus"           
##  [989] "Paralichthys oblongus"            "Paralichthys olivaceus"          
##  [991] "Paralichthys spp"                 "Paralithodes brevipes"           
##  [993] "Paralithodes camtschaticus"       "Paralithodes platypus"           
##  [995] "Paralithodes spp"                 "Paralomis aculeata"              
##  [997] "Paralomis formosa"                "Paralomis granulosa"             
##  [999] "Paralomis spinosissima"           "Paralomis spp"                   
## [1001] "Paralomis verrilli"               "Paralonchurus peruanus"          
## [1003] "Parapenaeopsis atlantica"         "Parapenaeopsis spp"              
## [1005] "Parapenaeus longirostris"         "Parapercis colias"               
## [1007] "Parapristipoma octolineatum"      "Parastromateus niger"            
## [1009] "Paratrachichthys trailli"         "Pareledone spp"                  
## [1011] "Parika scaber"                    "Paristiopterus labiosus"         
## [1013] "Parona signata"                   "Patagonotothen brevicauda"       
## [1015] "Patagonotothen ramsayi"           "Patinopecten caurinus"           
## [1017] "Patinopecten yessoensis"          "Pecten jacobaeus"                
## [1019] "Pecten maximus"                   "Pecten novaezelandiae"           
## [1021] "Pectinidae"                       "Pelates quadrilineatus"          
## [1023] "Pelecus cultratus"                "Pellona ditchela"                
## [1025] "Pellona flavipinnis"              "Pelotretis flavilatus"           
## [1027] "Penaeus aztecus"                  "Penaeus brasiliensis"            
## [1029] "Penaeus brevirostris"             "Penaeus californiensis"          
## [1031] "Penaeus chinensis"                "Penaeus duorarum"                
## [1033] "Penaeus indicus"                  "Penaeus japonicus"               
## [1035] "Penaeus kerathurus"               "Penaeus latisulcatus"            
## [1037] "Penaeus merguiensis"              "Penaeus monodon"                 
## [1039] "Penaeus notialis"                 "Penaeus occidentalis"            
## [1041] "Penaeus paulensis"                "Penaeus penicillatus"            
## [1043] "Penaeus schmitti"                 "Penaeus semisulcatus"            
## [1045] "Penaeus setiferus"                "Penaeus spp"                     
## [1047] "Penaeus stylirostris"             "Penaeus subtilis"                
## [1049] "Penaeus vannamei"                 "Pennahia anea"                   
## [1051] "Pennahia argentata"               "Pentaceros decacanthus"          
## [1053] "Pentanemus quinquarius"           "Peprilus paru"                   
## [1055] "Peprilus simillimus"              "Peprilus spp"                    
## [1057] "Peprilus triacanthus"             "Perciformes"                     
## [1059] "Percoidei"                        "Percophis brasiliensis"          
## [1061] "Perna perna"                      "Perna viridis"                   
## [1063] "Petromyzon marinus"               "Petromyzontidae"                 
## [1065] "Petrus rupestris"                 "Pharus legumen"                  
## [1067] "Phycis blennoides"                "Phycis chesteri"                 
## [1069] "Phycis phycis"                    "Phycis spp"                      
## [1071] "Pinguipes brasilianus"            "Pinguipes chilensis"             
## [1073] "Pitar rostratus"                  "Placopecten magellanicus"        
## [1075] "Plagiogeneion rubiginosum"        "Platax spp"                      
## [1077] "Platichthys flesus"               "Platichthys stellatus"           
## [1079] "Platycephalidae"                  "Platycephalus indicus"           
## [1081] "Plectorhinchus gaterinus"         "Plectorhinchus macrolepis"       
## [1083] "Plectorhinchus mediterraneus"     "Plectorhinchus pictus"           
## [1085] "Plectorhinchus schotaf"           "Plectorhinchus sordidus"         
## [1087] "Plectorhinchus spp"               "Plectropomus areolatus"          
## [1089] "Plectropomus leopardus"           "Plectropomus pessuliferus"       
## [1091] "Pleoticus muelleri"               "Pleoticus robustus"              
## [1093] "Plesionika martia"                "Plesiopenaeus edwardsianus"      
## [1095] "Pleuragramma antarcticum"         "Pleurogrammus azonus"            
## [1097] "Pleurogrammus monopterygius"      "Pleuroncodes monodon"            
## [1099] "Pleuroncodes planipes"            "Pleuronectes platessa"           
## [1101] "Pleuronectes quadrituberculat."   "Pleuronectes vetulus"            
## [1103] "Pleuronectidae"                   "Pleuronectiformes"               
## [1105] "Pleuronichthys decurrens"         "Plotosus spp"                    
## [1107] "Pogonias cromis"                  "Pogonophryne permitini"          
## [1109] "Pollachius pollachius"            "Pollachius virens"               
## [1111] "Pollicipes pollicipes"            "Polychaeta"                      
## [1113] "Polydactylus quadrifilis"         "Polymixia nobilis"               
## [1115] "Polynemidae"                      "Polyprion americanus"            
## [1117] "Polyprion oxygeneios"             "Pomacanthidae"                   
## [1119] "Pomacanthus maculosus"            "Pomadasys argenteus"             
## [1121] "Pomadasys incisus"                "Pomadasys jubelini"              
## [1123] "Pomadasys kaakan"                 "Pomadasys stridens"              
## [1125] "Pomatomus saltatrix"              "Pomatoschistus microps"          
## [1127] "Pontinus kuhlii"                  "Portunus pelagicus"              
## [1129] "Portunus spp"                     "Portunus trituberculatus"        
## [1131] "Priacanthus macracanthus"         "Priacanthus spp"                 
## [1133] "Prionace glauca"                  "Prionotus spp"                   
## [1135] "Pristidae"                        "Pristiophorus spp"               
## [1137] "Pristipomoides spp"               "Prolatilus jugularis"            
## [1139] "Promethichthys prometheus"        "Protemblemaria bicirris"         
## [1141] "Protothaca staminea"              "Protothaca thaca"                
## [1143] "Protrachypene precipua"           "Psenopsis anomala"               
## [1145] "Psetta maxima"                    "Psettichthys melanostictus"      
## [1147] "Psettodes belcheri"               "Psettodes erumei"                
## [1149] "Pseudocaranx dentex"              "Pseudocarcharias kamoharai"      
## [1151] "Pseudocardium sybillae"           "Pseudochaenichthys georgianus"   
## [1153] "Pseudocyttus maculatus"           "Pseudopentaceros richardsoni"    
## [1155] "Pseudopentaceros wheeleri"        "Pseudopercis semifasciata"       
## [1157] "Pseudophycis bachus"              "Pseudopleuronectes americanus"   
## [1159] "Pseudopleuronectes herzenst."     "Pseudotolithus elongatus"        
## [1161] "Pseudotolithus senegalensis"      "Pseudotolithus senegallus"       
## [1163] "Pseudotolithus spp"               "Pseudupeneus prayensis"          
## [1165] "Pterogymnus laniarius"            "Pteroscion peli"                 
## [1167] "Pterothrissus belloci"            "Pterygotrigla picta"             
## [1169] "Pterygotrigla polyommata"         "Puerulus sewelli"                
## [1171] "Rachycentron canadum"             "Raja alba"                       
## [1173] "Raja asterias"                    "Raja batis"                      
## [1175] "Raja brachyura"                   "Raja castelnaui"                 
## [1177] "Raja circularis"                  "Raja clavata"                    
## [1179] "Raja cyclophora"                  "Raja erinacea"                   
## [1181] "Raja fullonica"                   "Raja fyllae"                     
## [1183] "Raja georgiana"                   "Raja hyperborea"                 
## [1185] "Raja lintea"                      "Raja maderensis"                 
## [1187] "Raja microocellata"               "Raja miraletus"                  
## [1189] "Raja montagui"                    "Raja naevus"                     
## [1191] "Raja nidarosiensis"               "Raja oxyrinchus"                 
## [1193] "Raja radiata"                     "Raja spp"                        
## [1195] "Raja taaf"                        "Raja undulata"                   
## [1197] "Rajidae"                          "Rajiformes"                      
## [1199] "Rapana spp"                       "Rastrelliger brachysoma"         
## [1201] "Rastrelliger kanagurta"           "Rastrelliger spp"                
## [1203] "Regalecus glesne"                 "Reinhardtius hippoglossoides"    
## [1205] "Reptantia"                        "Rexea solandri"                  
## [1207] "Rhabdosargus globiceps"           "Rhabdosargus haffara"            
## [1209] "Rhinobatidae"                     "Rhinobatos cemiculus"            
## [1211] "Rhinobatos percellens"            "Rhinobatos planiceps"            
## [1213] "Rhinobatos rhinobatos"            "Rhinochimaera atlantica"         
## [1215] "Rhinoptera bonasus"               "Rhinoptera marginata"            
## [1217] "Rhizoprionodon acutus"            "Rhizoprionodon terraenovae"      
## [1219] "Rhomboplites aurorubens"          "Rhombosolea spp"                 
## [1221] "Rhopilema spp"                    "Rhynchobatus australiae"         
## [1223] "Rhynchobatus djiddensis"          "Rioraja agassizi"                
## [1225] "Ruditapes decussatus"             "Ruditapes philippinarum"         
## [1227] "Ruditapes spp"                    "Rutilus rutilus"                 
## [1229] "Rutilus spp"                      "Ruvettus pretiosus"              
## [1231] "Salilota australis"               "Salmo salar"                     
## [1233] "Salmo spp"                        "Salmo trutta"                    
## [1235] "Salmonoidei"                      "Salvelinus alpinus"              
## [1237] "Salvelinus spp"                   "Sarda chiliensis"                
## [1239] "Sarda orientalis"                 "Sarda sarda"                     
## [1241] "Sardina pilchardus"               "Sardinella aurita"               
## [1243] "Sardinella brasiliensis"          "Sardinella gibbosa"              
## [1245] "Sardinella lemuru"                "Sardinella longiceps"            
## [1247] "Sardinella maderensis"            "Sardinella spp"                  
## [1249] "Sardinella zunasi"                "Sardinops caeruleus"             
## [1251] "Sardinops melanostictus"          "Sardinops neopilchardus"         
## [1253] "Sardinops ocellatus"              "Sardinops sagax"                 
## [1255] "Sargocentron spiniferum"          "Sarpa salpa"                     
## [1257] "Saurida tumbil"                   "Saurida undosquamis"             
## [1259] "Saxidomus giganteus"              "Scapharca subcrenata"            
## [1261] "Scardinius erythrophthalmus"      "Scaridae"                        
## [1263] "Scarus ghobban"                   "Scarus persicus"                 
## [1265] "Scatophagus spp"                  "Schedophilus ovalis"             
## [1267] "Schedophilus pemarco"             "Schedophilus velaini"            
## [1269] "Sciaena umbra"                    "Sciaenidae"                      
## [1271] "Sciaenops ocellatus"              "Sclerocrangon spp"               
## [1273] "Scolopsis spp"                    "Scolopsis taeniata"              
## [1275] "Scomber australasicus"            "Scomber japonicus"               
## [1277] "Scomber scombrus"                 "Scomber spp"                     
## [1279] "Scomberesox saurus"               "Scomberoides commersonnianus"    
## [1281] "Scomberoides lysan"               "Scomberoides spp"                
## [1283] "Scomberoides tol"                 "Scomberomorus brasiliensis"      
## [1285] "Scomberomorus cavalla"            "Scomberomorus commerson"         
## [1287] "Scomberomorus guttatus"           "Scomberomorus lineolatus"        
## [1289] "Scomberomorus maculatus"          "Scomberomorus niphonius"         
## [1291] "Scomberomorus regalis"            "Scomberomorus sierra"            
## [1293] "Scomberomorus spp"                "Scomberomorus tritor"            
## [1295] "Scombridae"                       "Scombroidei"                     
## [1297] "Scophthalmidae"                   "Scophthalmus aquosus"            
## [1299] "Scophthalmus rhombus"             "Scorpaena porcus"                
## [1301] "Scorpaena scrofa"                 "Scorpaenichthys marmoratus"      
## [1303] "Scorpaenidae"                     "Scyliorhinidae"                  
## [1305] "Scyliorhinus canicula"            "Scyliorhinus spp"                
## [1307] "Scyliorhinus stellaris"           "Scylla serrata"                  
## [1309] "Scyllaridae"                      "Scyllarides aequinoctialis"      
## [1311] "Scyllarides latus"                "Scymnodon ringens"               
## [1313] "Sebastes alutus"                  "Sebastes crameri"                
## [1315] "Sebastes diploproa"               "Sebastes entomelas"              
## [1317] "Sebastes flavidus"                "Sebastes goodei"                 
## [1319] "Sebastes marinus"                 "Sebastes melanops"               
## [1321] "Sebastes mentella"                "Sebastes oculatus"               
## [1323] "Sebastes paucispinis"             "Sebastes pinniger"               
## [1325] "Sebastes spp"                     "Sebastes viviparus"              
## [1327] "Sebastolobus alascanus"           "Selachimorpha (Pleurotremata)"   
## [1329] "Selar crumenophthalmus"           "Selaroides leptolepis"           
## [1331] "Selene dorsalis"                  "Selene peruviana"                
## [1333] "Selene setapinnis"                "Selene vomer"                    
## [1335] "Semele solida"                    "Semicossyphus pulcher"           
## [1337] "Sepia officinalis"                "Sepia pharaonis"                 
## [1339] "Sepiidae, Sepiolidae"             "Sepioteuthis lessoniana"         
## [1341] "Sergestidae"                      "Seriola dumerili"                
## [1343] "Seriola fasciata"                 "Seriola lalandi"                 
## [1345] "Seriola rivoliana"                "Seriola spp"                     
## [1347] "Seriola zonata"                   "Seriolella brama"                
## [1349] "Seriolella caerulea"              "Seriolella porosa"               
## [1351] "Seriolella punctata"              "Seriolella spp"                  
## [1353] "Seriolina nigrofasciata"          "Serranidae"                      
## [1355] "Serranus atricauda"               "Serranus cabrilla"               
## [1357] "Serranus scriba"                  "Serranus spp"                    
## [1359] "Sicyonia brevirostris"            "Sicyonia ingentis"               
## [1361] "Siganus spp"                      "Siliqua patula"                  
## [1363] "Sillaginidae"                     "Sillago sihama"                  
## [1365] "Solea lascaris"                   "Solea senegalensis"              
## [1367] "Solea solea"                      "Soleidae"                        
## [1369] "Solen spp"                        "Solenidae"                       
## [1371] "Solenocera agassizii"             "Somniosus microcephalus"         
## [1373] "Somniosus pacificus"              "Somniosus rostratus"             
## [1375] "Sparidae"                         "Sparidentex hasta"               
## [1377] "Sparisoma cretense"               "Sparus aurata"                   
## [1379] "Sphoeroides maculatus"            "Sphoeroides spp"                 
## [1381] "Sphyraena barracuda"              "Sphyraena ensis"                 
## [1383] "Sphyraena jello"                  "Sphyraena obtusata"              
## [1385] "Sphyraena sphyraena"              "Sphyraena spp"                   
## [1387] "Sphyrna lewini"                   "Sphyrna tiburo"                  
## [1389] "Sphyrna zygaena"                  "Sphyrnidae"                      
## [1391] "Spicara maena"                    "Spicara smaris"                  
## [1393] "Spicara spp"                      "Spisula polynyma"                
## [1395] "Spisula solida"                   "Spisula solidissima"             
## [1397] "Spisula spp"                      "Spisula subtruncata"             
## [1399] "Spondyliosoma cantharus"          "Spratelloides gracilis"          
## [1401] "Sprattus fuegensis"               "Sprattus sprattus"               
## [1403] "Squalidae"                        "Squalidae, Scyliorhinidae"       
## [1405] "Squaliformes"                     "Squalus acanthias"               
## [1407] "Squalus blainville"               "Squalus spp"                     
## [1409] "Squatina argentina"               "Squatina californica"            
## [1411] "Squatina squatina"                "Squatinidae"                     
## [1413] "Squilla mantis"                   "Squillidae"                      
## [1415] "Stenotomus chrysops"              "Stephanolepis cirrhifer"         
## [1417] "Stereolepis gigas"                "Stichopus japonicus"             
## [1419] "Stolephorus spp"                  "Stomatopoda"                     
## [1421] "Stomolophus meleagris"            "Strangomera bentincki"           
## [1423] "Stromateidae"                     "Stromateus brasiliensis"         
## [1425] "Stromateus fiatola"               "Strombus spp"                    
## [1427] "Strongylocentrotus spp"           "Strongylura marina"              
## [1429] "Symphodus melops"                 "Sympterygia acuta"               
## [1431] "Sympterygia bonapartii"           "Synagrops japonicus"             
## [1433] "Synodontidae"                     "Synodus saurus"                  
## [1435] "Taractichthys steindachneri"      "Tautoga onitis"                  
## [1437] "Tautogolabrus adspersus"          "Tawera gayi"                     
## [1439] "Tellina spp"                      "Tenualosa ilisha"                
## [1441] "Tenualosa toli"                   "Terapon spp"                     
## [1443] "Tetraodontidae"                   "Tetrapturus albidus"             
## [1445] "Tetrapturus angustirostris"       "Tetrapturus audax"               
## [1447] "Tetrapturus belone"               "Tetrapturus georgii"             
## [1449] "Tetrapturus pfluegeri"            "Thaleichthys pacificus"          
## [1451] "Thelenota ananas"                 "Thenus orientalis"               
## [1453] "Theragra chalcogramma"            "Thunnus alalunga"                
## [1455] "Thunnus albacares"                "Thunnus atlanticus"              
## [1457] "Thunnus maccoyii"                 "Thunnus obesus"                  
## [1459] "Thunnus orientalis"               "Thunnus thynnus"                 
## [1461] "Thunnus tonggol"                  "Thymops birsteini"               
## [1463] "Thyrsites atun"                   "Thyrsitops lepidopoides"         
## [1465] "Tinca tinca"                      "Tivela mactroides"               
## [1467] "Todarodes filippovae"             "Todarodes pacificus"             
## [1469] "Todarodes sagittatus"             "Tonna galea"                     
## [1471] "Torpedo spp"                      "Totoaba macdonaldi"              
## [1473] "Trachichthyidae"                  "Trachinidae"                     
## [1475] "Trachinotus blochii"              "Trachinotus carolinus"           
## [1477] "Trachinotus mookalee"             "Trachinotus ovatus"              
## [1479] "Trachinotus spp"                  "Trachinus draco"                 
## [1481] "Trachinus spp"                    "Trachipterus arcticus"           
## [1483] "Trachipterus spp"                 "Trachipterus trachipterus"       
## [1485] "Trachurus capensis"               "Trachurus declivis"              
## [1487] "Trachurus japonicus"              "Trachurus lathami"               
## [1489] "Trachurus mediterraneus"          "Trachurus murphyi"               
## [1491] "Trachurus picturatus"             "Trachurus spp"                   
## [1493] "Trachurus symmetricus"            "Trachurus trachurus"             
## [1495] "Trachurus trecae"                 "Trachycardium muricatum"         
## [1497] "Trachypenaeus curvirostris"       "Trachyrincus scabrus"            
## [1499] "Trachyscorpia echinata"           "Tragulichthys jaculiferus"       
## [1501] "Trematomus eulepidotus"           "Trematomus spp"                  
## [1503] "Tresus spp"                       "Triakis megalopterus"            
## [1505] "Trichiuridae"                     "Trichiurus lepturus"             
## [1507] "Triglidae"                        "Tripterophycis gilchristi"       
## [1509] "Trisopterus esmarkii"             "Trisopterus luscus"              
## [1511] "Trisopterus minutus"              "Trochus niloticus"               
## [1513] "Turbo cornutus"                   "Tylosurus crocodilus"            
## [1515] "Tylosurus spp"                    "Ucides occidentalis"             
## [1517] "Umbrina canariensis"              "Umbrina canosai"                 
## [1519] "Umbrina cirrosa"                  "Upeneus spp"                     
## [1521] "Upogebia pugettensis"             "Uranoscopus scaber"              
## [1523] "Uranoscopus spp"                  "Urophycis brasiliensis"          
## [1525] "Urophycis chuss"                  "Urophycis tenuis"                
## [1527] "Valamugil seheli"                 "Variola louti"                   
## [1529] "Veneridae"                        "Venerupis pullastra"             
## [1531] "Venerupis rhomboides"             "Venus verrucosa"                 
## [1533] "Vimba vimba"                      "Xiphias gladius"                 
## [1535] "Xiphopenaeus kroyeri"             "Xiphopenaeus riveti"             
## [1537] "Xiphopenaeus, Trachypenaeus spp"  "Xyrichtys novacula"              
## [1539] "Zanclorhynchus spinifer"          "Zearaja nasuta"                  
## [1541] "Zeidae"                           "Zenopsis conchifer"              
## [1543] "Zenopsis nebulosus"               "Zeus faber"                      
## [1545] "Zidona dufresnei"                 "Zoarces viviparus"               
## [1547] "Zygochlamys delicatula"           "Zygochlamys patagonica"
```

17. Use the data to do at least one exploratory analysis of your choice. What can you learn?
+ I'm curious--what proportion of the data recorded is labelled 'Miscellaneous'?

```r
fisheries_tidy2 %>%
  filter(grepl('Miscellaneous', ISSCAAP_spgroupname)) %>%
  nrow()/nrow(fisheries_tidy2)
```

```
## [1] 0.3864793
```


## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
