---
layout: default
title: When to use RegEx
nav_order: 6
---
# Example of RegEx in action

## Look for matches in vector
We will use an example of a regular expression in R that is built into the tidyverse package. 

```r
## install tidyverse (only do this once on your computer)
install.packages("tidyverse)

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
## add a function to get all instances of duplcated a
fruits.re = str_replace_all(fruits, "a{2,}", function(x) {
  strrep("-", nchar(x) / 2) 
})
## output
fruits.re
```
This works, but what is the function doing? 
<a href="https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/strrep" target=_blank><em>strrep</em></a> make the str_replace_all frunction repeat to replace all the occurences of multiple "a" in the string.
<em>/2</em> is dividing that character count by 2 to avoid having on dash per extra "a". You can figure this out by adding more "a" in some places and seeing how there is more than one dash now.




## Special cases
### Look for matches, but exclude some based on a condition. 
### Periods
### Missign values (true NA) 
### Other replacement strategies
#### Base R
Functions in base R can do the same things as shown above. This means that are not part of a package that you need to install or load on your computer. Here is an example with gsub. 
```r
## fruits vector
fruits.re = c("one apple", "two pe-rs", "three b-n-nas")
## gsub to switch t to T
fruits.gs = gsub("t", "T", fruits.re)
fruits.gs
```
Here is an <a href="https://stringr.tidyverse.org/articles/from-base.html" target="_blank">equivalency table between stringr and base R</a>.
