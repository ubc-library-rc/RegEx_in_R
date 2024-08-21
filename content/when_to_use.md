---
layout: default
title: How and when to use regex
nav_order: 6
---
# Example of regex in action
Here, we use small vectors and dataframes to illustrate different replacement functions. Focus on how small changes in the regex syntax makes a big difference in the end result. These examples work both for vectors and dataframes, but we use mainly use vectors in these examples for simplicity. 

## Look for matches in vector
We will use an example of regex in R that is built into the tidyverse package (example for ?str_replace). 

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
In the fruits example, R looks in the the <em>fruits</em> vector for the letters within the [] <em>[aeiou]</em>. Anytime R finds any of the letters in [], it replaces them with a dash (-). This illustrates a critical part of regular expressions, "any matches" is the default way that the computer will look for matches. To get around this, you can make your expression more speicifc. For example, you could specify that the letters in [] should only be changed if they are after a space.

There are many symbols in regex syntax. The <a href="https://ubc-library-rc.github.io/intro-regex/content/03_basic_syntax.html#special-characters" target="_blank">general regex workshop</a> by the library has a wonderful table that summarizes common ones. 

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
See how here we are creating a new column <em>names.replaced</em> with the vowels replaced with a dash, but the <em>fruit.names</em> and <em>fruit.counts</em> do not have any dashes replacing vowels? This showcases targeted data manipulation within a dataframe. 

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
This works! When using regex, it is very important to check the output of your manipulations. 

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
Often, periods in data cause problems down the line for analysis, so it's nice to remove them. 

```r
## get the fruit vector
fruit = c("apple.", "pears.", "bananas.")
## try to replace a period (.) how we usually replace characters
fruit = str_replace(fruit, ".", "")

## this does not work!
## a period in regex means any character, so str_replace is replacing any first instance of a character (the first letter of the word in this case) with nothing.

## get values again
fruit = c("apple.", "pears.", "bananas.")
## escape the peiod 
fruit = str_replace(fruit, "\\.", "")

fruit
## yay!
```

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
View(fruits.df)
## right now, the NA in the fruit.counts column is not a true NA.
  ## We will convert it to a true NA here for the sake of this example
fruits.df$fruit.counts = as.numeric(fruits.df$fruit.counts)
## forcing fruit.counts from a character to numeric makes R replace the non number characters with missing values, NA. 
View(fruits.df)

## now that we have a missing value, let's deal with it by replacing the NA with the word "missing".
fruits.df$fruit.counts = str_replace_na(fruits.df$fruit.counts, "missing")
View(fruits.df)
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
Here is an <a href="https://stringr.tidyverse.org/articles/from-base.html" target="_blank">equivalency table between stringr and base R</a>. There is no computational reason to use tidyverse over base R. We are showcasing the operations in tidyverse in this workshop because tidyverse packages have very through documentation that tends to be more user freindly than base R documentation. You should feel free to use tidyverse and/or base R depending on what works best for the particular line of code you are currently wirting.
