---
title: "Regular Expressions basics"
teaching: 15
exercises: 10
questions:
- Use a few basic regular expressions. 
objectives:
- Understand the different elements of a regular expression
keypoints:
- Match caracters by using characters as a regex
- Add modifiers to change default behavior: case sensitive.
- Operators
---

## Scenario

You're working with a researcher who needs to locate information within a dataset she has collected. The researcher's data has been transcribed from field notebooks. Data was collected by a number of different grad students, and consists of site names, dates, and instrument readings. 

Each grad student's field notebook is saved as its own data file. There is little consistency between files, because each grad student recorded their information differently. Let's take a look:

Notebook 1:  

> Baker 1	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2009-11-17&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	1223.0  
> Baker 1	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2010-06-24&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	1122.7  
> Baker 2	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2009-07-24&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	2819.0  
> Baker 2	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2010-08-25&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	2971.6  
> Baker 1	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2011-01-05&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	1410.0  
> Baker 2	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2010-09-04&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	4671.6  
> ...  


Notebook 1 uses a single tab between each column as a separator. There are also spaces in the site names. The dates are written in the international standard format.

Notebook 2:

> Davison/May 23, 2010/1724.7  
> Pertwee/May 24, 2010/2103.8  
> Davison/June 19, 2010/1731.9  
> Davison/July 6, 2010/2010.7  
> Pertwee/Aug 4 2010/1731.3  
> Davison/Apr 22, 201/2122.2  
> Pertwee/Sept 3, 2010/3981.0  
> ...

Notebook 2 uses slashes as separators, and there are no spaces in the site names. Dates are in a non-standard format.

## Practice

* We will test our regular expressions using [Regex101](https://regex101.com)
* We need some data to search through. From the scenario above, let's assume that we've loaded all the data from notebook 1 and notebook 2 into one file for our analysis: [Download the sample data](../data/regex_data.txt)
* Open the sample data file, copy the contents, and paste it into the "Test String" box in Regex101

## Basics 

### Characters

* The core aspect of a regular expression is a set of one or more characters of text. Try putting a single character of text into the "Regular Expression" box on Regex101, for example: `a`
* The matched text will be highlighted in the "Test String" box
* The "Explanation" box tells you what the expression is doing
* Try a few other expressions, for example: `Baker`, `baker`, `24`,`04`, etc.


### Modifiers

* You likely noticed that your expressions in the previous section matched only the first occurance of that text, and that they were case sensitive. We can use modifiers to change this default behaviour.
* In Regex101 we add modifiers to the second box after the slash. Click on the question mark in that box and have a look at the help pop-up. 
* For now, let's use the `g` modifier. Optional: use the `i` modifier as well.
* Note: when using regex with a programming language, the syntax for this may differ. 

### Metacharacters & operators

There are certain characters that have special meaning in regular expressions, these are `\`, `|`, `(` `)` `.` `[` `]` `*` `+` `?` `{` `}` `^` `$`.

These are used in combination with text characters to construct regular expressions.

| Operator | Description | 
| ----------|-------------| 
| \ | Escape character - use when you need to include a metacharacter as a literal in a regular expression e.g. `\.txt` | 
| \| | OR (alternation) e.g. `wom[a|e]n`    | 
| ( ) | Group e.g. `(....)-(..)-(..)` for a date    | 
| . | Match any single character  e.g. `wom.n`     | 
| [abc] | Match any of a, b, or c. e.g. `[btr]ent` |
| [a-c] | Match any character between a and c. e.g. `[a-z]ent` |
| \* | The preceding item will be matched zero or more times e.g. `teen[a-z]*`    | 
| \+ | The preceding item will be matched one or more times `organi.+`     | 
| ? | The preceding item is optional and will be matched once at most, e.g. `colo?r` Used to make a quantifier 'lazy', e.g. `.+?` |
| {N} | The preceding item is matched exactly N times  `[0-9]{4}`    | 
| {N,} | The preceding item is matched N or more times  `[0-9]{4,}`    |
| {N,M} | The preceding item is matched at least N times, but not more than M times `[0-9]{4,6]`     |  
| ^ | Anchor: matches only at the start of the string e.g. `^b`  When used within a character set, negates the set, i.e. matches all characters *not* in the set - e.g. `[^abc]`      |  
| $ | Anchor: matches only at the end of the string e.g. `b$`      | 
| \b | Anchor: matches at "word boundary" (zero length position), i.e. transition from word to non-word characters. This allows you to perform "whole word only" searchers e.g. `\bword\b`
| \w | Shorthand character class: "word". Marches all the ASCII characters [A-Za-z0-9_] |
| \s | Shorthand character class: "whitespace". Matches non-word characters including space, tab, line break or form feed. |
| \d | Shorthand character class: "digit". Matches numeric characters [0-9]. |



### Building your first expressions 

* You want to find data from the month of June or July: `06|07` or `0(6|7)` (notice that when using the grouping operator, some information appears in the "Match" box in Regex101)  
* You want to find data from the month of May. What problem do you notice if you use the regex `05`? We need to take advantage of context. Try `-05-` instead.
* You want to match all dates that are in the international standard format: `....-..-..`  Another option is to use `(....)-(..)-(..)` which creates three groups, one for year, one for month, and one for day. This is handy when programmatically extracting data using regex
