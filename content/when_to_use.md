---
layout: default
title: When to use RegEx
nav_order: 6
---
# Example of RegEx in action
Here, we use the same vector to illustrate different replacement functions. Focus on how small changes in the vector or function used to replace characters makes a big difference in the end result. These examples work both for vectors and dataframes, but we use mainly use vectors in these examples for simplicity. 

## Look for matches in vector
We will use an example of a regular expression in R that is built into the tidyverse package. 

```r
## install tidyverse (only do this once on your computer)
install.packages("tidyverse")

## load tidyverse (do this every time you use R)
library(tidyverse)

## example from str_replace in stringr, a package in the package tidyverse
fruits = c("one apple", "two pears", "three bananas")
fruits
fruits.re = str_replace(fruits, "[aeiou]", "-")
fruits.re
```
### What is the computer doing here?
In the fruits example, R looks for the letters within the [] <em>[aeiou]</em> within the <em>fruits</em> vector. Anytime R finds any of the letters in [], it replaces them with a desh (-). This illustrates a critical part of regular expressions, "any matches" is the default way that the computer will look for matches. To get around this, you can exclude matches.

## Look for matches in a dataframe
Here, we are looking at one column in the dataframe instead of looking at a vector

```r
## get values
fruit.names = c("apple", "pears", "bananas")
fruit.counts = c("one", "two", "three")
## make data frame
fruits.df = data.frame(fruit.names, fruit.counts)
## replace vowels in the column fruit.names only
fruits.df$names.replaced = str_replace(fruits.df$fruit.names, "[aeiou]", "-")
```
See how here we are creating a new column <em>names.replaced</em> with the vowels replaced with a dash? This allows targeted data manipulation within a dataframe. 

## Multiple matches within the same string
Let's make a new fruit vector with some extra "a" letters and get rid of them.
Here we are adding some extra complexity as well. The {}, which are called curly brackets, with the <em>2,</em> inside of them is telling str_replace to only replace instances where there are at least 2 "a" in a row. So replace "aa", "aaa", "aaaa", and so on, but not "a" surrounded by other letters.

```r
## fruit vector
fruits = c("one apple", "two peaars", "three baaanaaanas")
## attempt 1 
fruits.re = str_replace(fruits, "a{2,}", "-")
## output
fruits.re
```
There is a problem though, this is the output <em> "one apple"       "two pe-rs"       "three b-naaanas" </em>. What is going on here? str_replace only looks for the first instance of a match in a string. How do we get around this?

```r
## fruit vector
fruits = c("one apple", "two peaars", "three baaanaaanas")
## attempt 2 
fruits.re = str_replace_all(fruits, "a{2,}", "-")
## output
fruits.re
```
This works! When using RegEx, it is very important to check the output of your manipulations. 

## Look for matches that match a condition that includes many characters. 
Sometimes, there are too many characters to list in a replacement target list, but they all meet a condition. In this case, let's replace all numbers with a dash.

```r
## fruit vector
fruits = c("0ne appl3", "tw0 p3ars", "thr33 bananas")
## attempt 1 
fruits.re = str_replace_all(fruits, "[:digit:]", "-")
## output
fruits.re
```


## Special cases
### Periods
### Missing values (true NA) 
The purposes of this section is:
1. To be able to tell the difference between cells that say NA and what the missing value (NA) in R looks like. They are not the same and this tends to cause confusion. 
2. To teach you how to deal with real missing values.

```r
## get values
fruit.names = c("apple", "pears", "bananas")
fruit.counts = c("1", "2", "NA")
## make data frame
fruits.df = data.frame(fruit.names, fruit.counts)
## right now, the NA in the fruit.counts column is not a true NA. We will convert it to a true NA here for the sake of this example
fruits.df$fruit.counts = as.numeric(fruits.df$fruit.counts)
## forcing fruit.counts from a character to numeric makes R replace the non number characters with missing values, NA. 

## now that we have a missing value, let's deal with it
fruits.df$fruit.counts = str_replace_na(fruits.df$fruit.counts, "missing")
```

## Base R
Functions in base R can do the same things as shown above. This means that are not part of a package that you need to install or load on your computer. Here is an example with gsub. 
```r
## fruits vector
fruits.re = c("one apple", "two pe-rs", "three b-n-nas")
## gsub to switch t to T
fruits.gs = gsub("t", "T", fruits.re)
fruits.gs
```
Here is an <a href="https://stringr.tidyverse.org/articles/from-base.html" target="_blank">equivalency table between stringr and base R</a>.
