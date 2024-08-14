---
layout: default
title: What are regular expressions?
nav_order: 4
---
# Defining regex
"Regular expressions are a powerful and standardized way of representing patterns in text using special symbols and syntax." - <a href="https://ubc-library-rc.github.io/intro-regex/" target="_blank">UBC Research Commons (UBC library)</a>

"A regular expression, regex, in R is a sequence of characters (or even one character) that describes a certain pattern found in a text." - <a href="https://www.datacamp.com/tutorial/regex-r-regular-expressions-guide" target="_blank">Data Camp </a>

"Regular expressions are a concise and flexible tool for describing patterns in strings." - <a href="https://cran.r-project.org/web/packages/stringr/vignettes/regular-expressions.html" target="_blank">CRAN</a>

# Use cases
## When to use regex
To clean up strings (text) before analysis. After cleaning up the strings, finding macthes between groups and linking different strings will be much easier. 

## When might regex not be appropriate
If you are unfamiliar with the dataset. The important first step for efficient regex implementation is understanding the variation in your data. Getting this wrong could lead to not aggregetating strings that need to be aggreagated, or aggregating string that should be seperate. 

For example, pretend you are working with linguistics data (workshop for this comming soon!), is the difference between <em>color</em> and <em>colour</em> meaningful? These types of questions are critical when setting up the regex and depend on your research question/goal. 


