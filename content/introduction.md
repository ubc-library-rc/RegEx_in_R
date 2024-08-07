---
layout: default
title: What are regular expressions?
nav_order: 4
---
# Defining RegEx
"A regular expression, regex, in R is a sequence of characters (or even one character) that describes a certain pattern found in a text." - <a href="https://www.datacamp.com/tutorial/regex-r-regular-expressions-guide" target="_blank">Data Camp </a>

"Regular expressions are a concise and flexible tool for describing patterns in strings." - <a href="https://cran.r-project.org/web/packages/stringr/vignettes/regular-expressions.html" target="_blank">CRAN</a>

"Regular expressions are a syntax for matching patterns in text. <strong>They allow us to detect, extract, replace, or remove text that satisfies a certain pattern, rather than just an exact string</strong>." - <a href="https://jfjelstul.github.io/regular-expressions-tutorial/" target="_blank">J. Fjelstul</a>

# Use cases
## When to use RegEx
To clean up strings (text) before analysis. After cleaning up the strings, finding macthes between groups and linking different strings will be much easier. 

## When might RegEx not be appropriate
1. RegEx are useful for strings. This means characters (text). True missing values (<em>NA</em>), are not the same as a cell in your data containing the string "NA". This difference is important and the combination of RegEx with other tools may be necessary.
2. If you are unfamiliar with the dataset. The important first step for efficient RegEx implementation is understanding the variation in your data. Getting this wrong could lead to not aggregetating strings that need to be aggreagated, or aggregating string that should be seperate. For example, pretend you are working with linguistics data (workshop for this comming soon!), is the difference between <em>color</em> and <em>colour</em> meaningful? 


