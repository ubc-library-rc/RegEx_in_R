---
layout: default
title: RegEx Practice
nav_order: 7
---
# List of practice problems 

## Single letter

## Groups of letters

## Combinations of words

## Excluding potential matches from being changed

## Multi-step problems
These probelms are meant to be challenging and require multiple steps to complete.

``` r
## values
dates = c("2000-03-08", "2001-3-15", "2002-03-21", "2003-March -12", "2004-mar-3", "2004-0 3-17")
collection_id = c("c1 ", "c2 ", "c3", "c4 ", "c5", "c6")
deposited = c("yes", "y", "yes", " yes", "Yes ", "no")
## make dataframe 
herbarium_inventory = as.data.frame(cbind(dates, collection_id, deposited))
```
Fix the herbarium_inventory to 
1. Not have any spaces
2. Convert the deposited to <em>1</em> for all the vairations of yes and <em>0</em> for no
3. Convert all the permutations of the month March to be written as <em>March</em>

<details><summary><strong> Answer </strong></summary>

1. Remove all spaces
<p>herbarium_inventory <- str_replace_all(" ", "", herbarium_inventory)</p>

2. Convert the "deposited" column to 1 for "yes" and 0 for "no"
<p>herbarium_inventory$deposited <- ifelse(grepl("y(es)", herbarium_inventory$deposited), 1, 0)</p>

3. Fix month
<p>herbarium_inventory$dates <- gsub("-(0?3-|(?i)mar)-", "-March-", herbarium_inventory$dates)</p>

</details>

