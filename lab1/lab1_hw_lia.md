---
title: "Lab 1 Homework"
author: "What is Your Name?"
date: "Winter 2020"
output:
  html_document: 
    keep_md: yes
    theme: spacelab
---

## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code, keep track of your versions using git, and push your final work to our [GitHub repository](https://github.com/FRS417-DataScienceBiologists). I will randomly select a few examples of student work at the start of each session to use as examples so be sure that your code is working to the best of your ability.  

1. Navigate to the R console and calculate the following expressions.  
  + 5 - 3 * 2 
  == -1
  + 8 / 2 ** 2
  == 2
  
2. Did any of the results in #1 surprise you? Write two programs that calculate each expression such that the result for the first example is 4 and the second example is 16.

```r
(5 - 3) * 2
```

```
## [1] 4
```

```r
(8/2)^2
```

```
## [1] 16
```


3. Make a new object `pi` as 3.14159265359.

```r
pi <- 3.14159265359
```


4. Is `pi` an integer or numeric? Why? Show your code.  

```r
class(pi)
```

```
## [1] "numeric"
```
this is numeric, it is not a whole number

5. You have decided to use your new analytical powers in R to become a professional gambler. Here are your winnings and losses this week. Note that you don't gamble on the weekends!  

```r
blackjack <- c(140, -20, 70, -120, 240, NA, NA)
roulette <- c(60, 50, 120, -300, 10, NA, NA)
```

a. Build a new vector called `days` for the days of the week. 

```r
days <- c("Monday", "Tuesday", "Wednesday", "Thrusday", "Friday", "Saturday", "Sunday")
```


We will use `days` to name the elements in the poker and roulette vectors.

```r
names(blackjack) <- days
names(roulette) <- days
```

b. Calculate how much you won or lost in blackjack over the week.  

```r
sum(blackjack)
```

```
## [1] NA
```


c. What is your interpretation of this result? What do you need to do to address the problem? Recalculate how much you won or lost in blackjack over the week.  
I first did not specify that the NA values for the weekend should be removed. I did so in the following.


```r
sum(blackjack, na.rm = TRUE)
```

```
## [1] 310
```


d. Calculate how much you won or lost in roulette over the week.  


```r
sum(roulette, na.rm = TRUE)
```

```
## [1] -60
```


e. Build a `total_week` vector to show how much you lost or won on each day over the week. Which days seem lucky or unlucky for you?


```r
total_week <- c(blackjack[1] + roulette[1], blackjack[2] + roulette[2], blackjack[3] + roulette[3],
                blackjack[4] + roulette[4], blackjack[5] + roulette[5])
```
It looks like Friday was our lucky day winning 250 and Thursday our least luckiest losing 420.

f. Should you stick to blackjack or roulette? Write a program that verifies this below.  

```r
blackjack_winnings <- sum(blackjack, na.rm = TRUE)
roulette_winnings <- sum(roulette, na.rm = TRUE)
if(blackjack_winnings > roulette_winnings){
  print("Stick to blackjack")
} else {
  print("Stick to roulette")
}
```

```
## [1] "Stick to blackjack"
```
We should stick to blackjack.

## Push your final code to [GitHub](https://github.com/FRS417-DataScienceBiologists)