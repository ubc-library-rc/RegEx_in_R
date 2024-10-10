---
layout: default
title: RegEx Practice
nav_order: 7
---
# List of practice problems 
All of these problems are set up in the same way. You are given code to set up the problem, and then it's up to you to work from there to get to the solution.

We also use these practice problems to introduce topics not covered in the "lecture" part of the workshop, so you will need to look up how to do most of these exercises, which is what you will have to do when using your own dataset.

The idea is not to solve the probelm the same way that is here. The important thing is to get the same result, which is why we provide answer code. There are many ways to get both correct and wrong answers, so check the output carefully. 

## I - Single letter
### P1 - Replace all "-" with "a" (vector)
``` r
## starting vector
fruits <- c("one -pple", "two pe-rs", "three b-n-n-s")
```
<details><summary><strong> Answer </strong></summary>
        fruits = str_replace_all(fruits, "-", "a")
</details>

### P2 - Replace "-" with "e" in the count column only
``` r
## get vector
fruit = c("appl-", "apricot", "b-ll p-pp-r")
count = c("on-", "two", "thr--")
## make dataframe
fruitcount = as.data.frame(cbind(fruit, count))
```
<details><summary><strong> Answer </strong></summary>
        fruitcount$count = gsub("-", "e", fruitcount$count)
</details>

## II - Groups of letters
### P1 - Replace all vowels with "-"
This is an example from stringr, type ?str_replace to find it in the help tab.

``` r
## get vector
fruits <- c("one apple", "two pears", "three bananas")
```
<details><summary><strong> Answer </strong></summary>
        fruits = str_replace_all(fruits, "[aeiou]", "-")
</details>

### P2 - Capitalize first letter of each word
``` r
## get vector
fruits <- c("one apple", "two pears", "three bananas")
```
<details><summary><strong> Answer </strong></summary>
        fruits = str_to_title(fruits)
</details>


## III - Combinations of words
### P1 - remove the end of the words that are Amarica and British english and sigular or plural
Your goal is for <em>length(unique(words))</em> to output 2. Right now, it outputs 8. 

``` r
## initial vector of words
words = c("color", "colour", "flavor", "flavour", "colors", "colours", "flavors", "flavours")

## how many unique words?
length(unique(words))
        # 8 words
```
<details><summary><strong> Answer </strong></summary>
        words = str_replace(words, "o(u)*r(s)*", "")
</details>


## IV - Excluding potential matches from being changed
### P1 - convert all letters to "-" except "e"
``` r
fruits <- c("one apple", "two pears", "three bananas")
```
<details><summary><strong> Answer </strong></summary>
        fruits = str_replace_all(fruits, "[a-d,f-z]", "-")
</details>


## V - Most complex problems

### P1 - Herbarium inventory dataset
``` r
## values
dates = c("2000-03-08", "2001-3-15", "2002-03-21", "2003-March -12", "2004-mar-3", "2004-0 3-17")
collection_id = c("c1 ", "c2 ", "c3", "c4 ", "c5", "c6")
deposited = c("yes", "y", "yes", " yes", "Yes ", "no")
## make dataframe 
herbarium_inventory = as.data.frame(cbind(dates, collection_id, deposited))
```
Fix the herbarium_inventory to 
1. Not have any spaces.
2. Convert all te variatons of yes to <em>1</em> all the no to <em>0</em>.
3. Convert all the permutations of the month March to be written as <em>March</em>.

<details><summary><strong> Answer </strong></summary>

1. Remove all spaces
       <p>herbarium_inventory <- str_replace_all(" ", "", herbarium_inventory)</p>
2. Convert the "deposited" column to 1 for "yes" and 0 for "no"
      <p>herbarium_inventory$deposited <- ifelse(grepl("y(es)", herbarium_inventory$deposited), 1, 0)</p>  
3. Fix month
        <p>herbarium_inventory$dates <- gsub("-(0?3-|(?i)mar)-", "-March-", herbarium_inventory$dates)</p>

</details>

### P2 - set up data for the start of problem I-P2
Start with a nice dataset and change every "e" to "-"

``` r
## vectors
fruit = c("apple", "apricot", "bell pepper")
count = c("one", "two", "three")
## make dataframe 
fruitcount = as.data.frame(cbind(fruit, count))
```
<details><summary><strong> Answer </strong></summary>
        fruitcount = data.frame(lapply(fruitcount, gsub, pattern = "e", replacement = "-", fixed = TRUE))
</details>

### P3 - Edit URLs

``` r
## starting url list
url = c("https://www2.gov.bc.ca/gov/content/home", 
        "https://www.canada.ca/en.html", 
        "https://yukon.ca/", 
        "https://www.alberta.ca/")
```
Your target is to have this url list <em>"gov.bc"  "canada"  "yukon"   "alberta"</em>

<details><summary><strong> Answer </strong></summary>

1. get rid of the parts of the very start of the urls
        <p>url.short = gsub("https://", "", url)</p>
2. get rid of the rest of the start start of URLs that is not interesting rigth now
       <p>url.short = gsub("(www|www2)(\\.)", "", url.short)</p>
3. get rid of .ca and everything at the end</p>
      <p>url.short = gsub("\\.ca.*", "", url.short)</p>  

</details>

