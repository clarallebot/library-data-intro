---
title: "Regular expressions exercises"
teaching: 45
exercises: 17
questions:
- Exercises to solve together
objectives:
- Understand how to modify a regular expression to select the desired kind of text.
keypoints:
- Select upper case or lower case; match any character; assert the position at the start and end of line; add a word boundary
---


## Summary


Square brackets can be used to define a list or range of characters to be found. So:

- `[ABC]` matches A or B or C
- `[A-Z]` matches any upper case letter
- `[A-Za-z]` matches any upper or lower case letter (note: this is case-sensitive)
- `[A-Za-z0-9]` matches any upper or lower case letter or any digit (note: this is case-sensitive)

Then there are:

- `.` matches any character
- `\d` matches any single digit
- `\w` matches any part of word character (equivalent to `[A-Za-z0-9]`)
- `\s` matches any space, tab, or newline
- `\` NB: this is also used to escape the following character when that character is a special character. So, for example, a regular expression that found `.com` would be `\.com` because `.` is a special character that matches any character.
- `^` asserts the position at the start of the line. So what you put after the caret will only match if they are the first characters of a line. The caret is also known as a circumflex.
- `$` asserts the position at the end of the line. So what you put before it will only match if they are the last characters of a line.
- `\b` adds a word boundary. Putting this either side of a word stops the regular expression matching longer variants of words. So:
	- the regular expression `foobar` will match `foobar` and find `666foobar`, `foobar777`, `8thfoobar8th` et cetera
	- the regular expression `\bfoobar` will match `foobar` and find `foobar777`
	- the regular expression `foobar\b` will match `foobar` and find `666foobar`
	- the regular expression `\bfoobar\b` will find `foobar`
	
Other useful special characters are:

- `*` matches the preceding element zero or more times. For example, ab*c matches "ac", "abc", "abbbc", etc.
- `+` matches the preceding element one or more times. For example, ab+c matches "abc", "abbbc" but not "ac".
- `?` matches when the preceding character appears zero or one time.
- `{VALUE}` matches the preceding character the number of times defined by VALUE; ranges, say, 1-6, can be specified with the syntax `{VALUE,VALUE}`, e.g. `\d{1,9}` will match any number between one and nine digits in length.
- `|` means or.
- `/i` renders an expression case-insensitive (equivalent to `[A-Za-z]`)

## Exercises

A very simple use of a regular expression would be to locate the same word spelled two different ways. For example the regular expression `organi[sz]e` matches both "organise" and "organize".

But it would also match `reorganise`, `reorganize`, `organises`, `organizes`, `organised`, `organized`, et cetera, because we have not specified the beginning or end of our string. So we need to use special syntax to help us be more precise.

We will continue using [regex101.com/](https://regex101.com/) to test our solutions. Copy and paste the data in [regex_exercises_data.txt](../data/regex_exercises_data.txt) under "test string". Select the flag 'm' (multiline) and the flag 'g' (global) so that you will get more than one match in one line, and matches in different lines and so that ^ and $ will match the start/end of the line. 

So, what is `^[Oo]rgani.e\b` going to match?

> ## Using special characters in regular expression matches
> Can you guess what the regular expression `^[Oo]rgani.e\b` will match?
>
> > ## Solution
> > ~~~
> > organise
> > organize
> > Organise
> > Organize
> > organife
> > Organike
> > ~~~
> > Or, any other string that starts a line, begins with a letter `o` in lower or capital case, proceeds with `rgani`, has any character in the 7th position, and ends with the letter `e`.
> {: .solution}
{: .challenge}



So, what are these going to match?

> ## ^[Oo]rgani.e\w*
> Can you guess what the regular expression `^[Oo]rgani.e\w*` will match?
>
> > ## Solution
> > ~~~
> > organise
> > Organize
> > organifer
> > Organi2ed111
> > ~~~
> > Or, any other string that starts a line, begins with a letter `o` in lower or capital case, proceeds with `rgani`, has any character in the 7th position, follows with letter `e` and zero or more characters from the range `[A-Za-z0-9]`.
> {: .solution}
{: .challenge}

> ## [Oo]rgani.e\w+$
> Can you guess what the regular expression `[Oo]rgani.e\w+$` will match?
>
> > ## Solution
> > ~~~
> > organiser
> > Organized
> > organifer
> > Organi2ed111
> > ~~~
> > Or, any other string that ends a line, begins with a letter `o` in lower or capital case, proceeds with `rgani`, has any character in the 7th position, follows with letter `e` and **at least one or more** characters from the range `[A-Za-z0-9]`.
> {: .solution}
{: .challenge}

> ## ^[Oo]rgani.e\w?\b
> Can you guess what the regular expression `^[Oo]rgani.e\w?\b` will match?
>
> > ## Solution
> > ~~~
> > organise
> > Organized
> > organifer
> > Organi2ek
> > ~~~
> > Or, any other string that starts a line, begins with a letter `o` in lower or capital case, proceeds with `rgani`, has any character in the 7th position, follows with letter `e`, and ends with **zero or one** characters from the range `[A-Za-z0-9]`.
> {: .solution}
{: .challenge}

> ## ^[Oo]rgani.e\w?$
> Can you guess what the regular expression `^[Oo]rgani.e\w?$` will match?
>
> > ## Solution
> > ~~~
> > organise
> > Organized
> > organifer
> > Organi2ek
> > ~~~
> > Or, any other string that starts and ends a line, begins with a letter `o` in lower or capital case, proceeds with `rgani`, has any character in the 7th position, follows with letter `e` and **zero or one characters** from the range `[A-Za-z0-9]`.
> {: .solution}
{: .challenge}

> ## \b[Oo]rgani.e\w{2}\b
> Can you guess what the regular expression `\b[Oo]rgani.e\w{2}\b` will match?
>
> > ## Solution
> > ~~~
> > organisers
> > Organizers
> > organifers
> > Organi2ek1
> > ~~~
> > Or, any other string that begins with a letter `o` in lower or capital case after a word boundary, proceeds with `rgani`, has any character in the 7th position, follows with letter `e`, and ends with **two** characters from the range `[A-Za-z0-9]`.
> {: .solution}
{: .challenge}

> ## \b[Oo]rgani.e\b|\b[Oo]rgani.e\w{1}\b
> Can you guess what the regular expression `\b[Oo]rgani.e\b|\b[Oo]rgani.e\w{1}\b` will match?
>
> > ## Solution
> > ~~~
> > organise
> > Organi1e
> > Organizer
> > organifed
> > ~~~
> > Or, any other string that begins with a letter `o` in lower or capital case after a word boundary, proceeds with `rgani`, has any character in the 7th position, and end with letter `e`, or any other string that begins with a letter `o` in lower or capital case after a word boundary, proceeds with `rgani`, has any character in the 7th position, follows with letter `e`, and ends with a single character from the range `[A-Za-z0-9]`.
> {: .solution}
{: .challenge}

This logic is useful when you have lots of files in a directory, when those files have logical file names, and when you want to isolate a selection of files. Or it can be used for looking at cells in spreadsheets for certain values, or for extracting some data from a column of a spreadsheet to make  new columns. I could go on. The point is, it is useful in many contexts. To embed this knowledge we won't - however - be using computers. Instead we'll use pen and paper. Work in teams of 4-6 on the exercises below. When you think you have the right answer, check it against the solution. When you finish, I'd like you to split your team into two groups and write each other some tests. These should include a) strings you want the other team to write regex for and b) regular expressions you want the other team to work out what they would match. Then test each other on the answers. If you want to check your logic, use [regex101](https://regex101.com/), [myregexp](http://myregexp.com/), or [regex pal](http://www.regexpal.com/) [regexper.com](http://regexper.com/): the first three help you see what text your regular expression will match, the latter visualises the workflow of a regular expression.

### Exercise

Pair up with the person next to you to work through the following problems.

> ## Using square brackets
> Can you guess what the regular expression `Fr[ea]nc[eh]` will match?
>
> > ## Solution
> > ~~~
> > French
> > France
> > Frence
> > Franch
> > ~~~
> > This will also find words where there are characters either side of the solutions above, such as `Francer`, `foobarFrench`, and `Franch911`.
> {: .solution}
{: .challenge}

> ## Using dollar signs
> Can you guess what the regular expression `Fr[ea]nc[eh]$` will match?
>
> > ## Solution
> > ~~~
> > French
> > France
> > Frence
> > Franch
> > ~~~
> > This will also find strings at the end of a line. It will find words where there were characters before these, for example `foobarFrench`.
> {: .solution}
{: .challenge}

> ## Introducing options
> What would match the strings `French` and `France` only that appear at the beginning of a line?
>
> > ## Solution
> > ~~~
> > ^France|^French
> > ~~~
> > This will also find words where there were characters after `French` such as `Frenchness`.
> {: .solution}
{: .challenge}

> ## Case insensitivity
> How do you match the whole words `colour` and `color` (case insensitive)?
>
> > ## Solutions
> > ~~~
> > \b[Cc]olou?r\b|\bCOLOU?R\b
> > /colou?r/i
> > ~~~
> > In real life, you *should* only come across the case insensitive variations `colour`, `color`, `Colour`, `Color`, `COLOUR`, and `COLOR` (rather than, say, `coLour`). So based on what we know, the logical regular expression is `\b[Cc]olou?r\b|\bCOLOU?R\b`. An alternative more elegant option we've not discussed is to take advantage of the `/` delimiters and add an 'ignore case' flag: so `/colou?r/i` will match all case insensitive variants of `colour` and `color`.
> {: .solution}
{: .challenge}

> ## Word boundaries
> How would you find the whole word `headrest` and or `head rest` but not `head  rest` (that is, with two spaces between `head` and `rest`?
>
> > ## Solution
> > ~~~
> > \bhead ?rest\b
> > ~~~
> > Note that although `\bhead\s?rest\b` does work, it will also match zero or one tabs or newline characters between `head` and `rest`. So again, although in most real world cases it will be fine, it isn't strictly correct.
> {: .solution}
{: .challenge}

> ## Matching non-linguistic patterns
> How would you find a string that ends with 4 letters preceded by at least one zero?
>
> > ## Solution
> > ~~~
> > 0+[A-Za-z]{4}\b
> > ~~~
> {: .solution}
{: .challenge}

> ## Matching digits
> How do you match any 4-digit string anywhere?
>
> > ## Solution
> > ~~~
> > \d{4}
> > ~~~
> > Note: this will also match 4 digit strings within longer strings of numbers and letters.
> {: .solution}
{: .challenge}

> ## Matching dates
> How would you match the date format `dd-MM-yyyy`?
>
> > ## Solution
> > ~~~
> > \b\d{2}-\d{2}-\d{4}\b
> > ~~~
> > Depending on your data, you may chose to remove the word bounding.
> {: .solution}
{: .challenge}

> ## Matching multiple date formats
> How would you match the date format `dd-MM-yyyy` or `dd-MM-yy` at the end of a line only?
>
> > ## Solution
> > ~~~
> > \d{2}-\d{2}-\d{2,4}$
> > ~~~
> > Note this will also find strings such as `31-01-198` at the end of a line, so you may wish to check your data and revise the expression to exclude false positives. Depending on your data, you may chose to add word bounding at the start of the expression.
> {: .solution}
{: .challenge}

> ## Matching publication formats
> How would you match publication formats such as `British Library : London, 2015` and `Manchester University Press: Manchester, 1999`?
>
> > ## Solution
> > ~~~
> > .* ?: .*, \d{4}
> > ~~~
> > Without word boundaries you will find that this matches any text you put before `British` or `Manchester`. Nevertheless, the regular expression does a good job on the first look up and may be need to be refined on a second, depending on your data.
> {: .solution}
{: .challenge}
