---
title: "Introduction to Regular Expressions"
teaching: 10
exercises: 0
questions:
- How can you imagine using regular expressions in your work?
objectives:
- Use regular expressions in searches
keypoints:
- Regular expressions are powerful tools for pattern matching
- "Check your regex with: regex101 [https://regex101.com/](https://regex101.com/), rexegper [http://regexper.com/](http://regexper.com/), or myregexp [http://myregexp.com/]([http://myregexp.com/])."
- "Test yourself with: Regex Crossword [https://regexcrossword.com/](https://regexcrossword.com/) or our The Multiple Choice Quiz [http://data-lessons.github.io/library-data-intro/05-quiz/](http://data-lessons.github.io/library-data-intro/05-quiz/)."
---

## Regular Expressions

One of the reasons we stress the value of consistent and predictable directory and filenaming conventions is that working in this way enables you to use the computer to select files based on the characteristics of their file names. So, for example, if you have a bunch of files where the first four digits are the year and you only want to do something with files from '2017', then you can. Or if you have 'journal' somewhere in a filename when you have data about journals, you can use the computer to select just those files, then do something with them. Equally, using plain text formats means that you can go further and select files or elements of files based on characteristics of the data *within* those files.

A powerful means of doing this selecting based on file characteristics is to use regular expressions, often abbreviated to *regex*. A regular expression is a sequence of characters that define a search pattern, mainly for use in pattern matching with strings, or string matching, i.e. "find and replace"-like operations. For those who have not met this term before, a string is a contiguous sequence of symbols or values, for example, a word, a date, a set of numbers, such as a phone numnber, or an alphanumeric value such as a repository identifier.

Regular expressions are typically surrounded by `/` characters, though we will (mostly) ignore those for ease of comprehension. Regular expressions will let you:

- Match on types of character (e.g. 'upper case letters', 'digits', 'spaces', etc.)
- Match patterns that repeat any number of times
- Capture the parts of the original string that match your pattern

As most computational software has regular expression functionality built in and as many computational tasks in libraries are built around complex matching, it is good place for Library Carpentry to start in earnest.

Warning: regex notation is ugly! This is because we're writing patterns to match strings, but we're writing those patterns as strings...using only the symbols on the keyboard (instead of inventing new symbols the way mathematicians do).

## Examples of when to use Regular Expressions

The more you use regular expressions, the more you realize that you can use them everywhere! These are some examples of contexts that you probably encounter often, where you can take advantage of regular expressions:

* Text editors, such as Notepad ++, Sublime, Atom, vim...
* The find and replace feature in spreadsheets, like Excel and Google Sheets. To do this, you need to select the "Search using regular expressions" box. 
* The find and replace feature in Open Office and Microsoft Word.
* When using Open Refine, as you can see in the [Open Refine Library Carpentry lesson](http://data-lessons.github.io/library-openrefine/reference)!
* From the command line. For example, to select file names with `ls | grep "regularexpression"`

## References

James Baker , "Preserving Your Research Data," *Programming Historian* (30 April 2014), [http://programminghistorian.org/lessons/preserving-your-research-data.html](http://programminghistorian.org/lessons/preserving-your-research-data.html). The sub-sections 'Plain text formats are your friend' and 'Naming files sensible things is good for you and for your computers' are reworked from this lesson.

Owen Stephens, "Working with Data using OpenRefine", *Overdue Ideas" (19 November 2014), [http://www.meanboyfriend.com/overdue_ideas/2014/11/working-with-data-using-openrefine/](http://www.meanboyfriend.com/overdue_ideas/2014/11/working-with-data-using-openrefine/). The section on 'Regular Expressions' is reworked from this lesson developed by Owen Stephens on behalf of the British Library

Andromeda Yelton, "Coding for Librarians: Learning by Example", *Library Technology Reports* 51:3 (April 2015), doi: [10.5860/ltr.51n3](http://dx.doi.org/10.5860/ltr.51n3)

Fiona Tweedie, "Why Code?", *The Research Bazaar* (October 2014), [http://melbourne.resbaz.edu.au/post/95320810834/why-code](http://melbourne.resbaz.edu.au/post/95320810834/why-code)
