---
title: "Quantifiers in Regular Expressions"
teaching: 15
exercises: 0
questions:
- How do I slect text using regex?
objectives:
- Learn the use of quantifiers to match text with regex
keypoints:
- Use \ to escape a special character
- Use * to match zero or more characters
- Use + to match one or more characters
- Use ? for making an operator optional 
- Use {} to specify how many times something will occur, or a range
---

## Quantifiers

Let's work through a more involved example that introduces a number of operators that fall under the category of "quantifiers". Quantifiers specify how many instances of a character, group, or character set must be present (we'll talk about what a character set is later).

It was straightforward to match all the standardized dates, but what about matching all the dates that are in the unstandardized text format? Let's break this task into steps:

1. First of all, try to match a `/` using Regex101. It won't let you do it, because the regex syntax requires this character to mark the beginning and the end of the expression. You need to escape the slash character. Try `\/`. 
2. Now we want to match all the text between two slashes. We don't know exactly how many characters there are, because the month and days have variable number of characters in them. We can use the `*` character to match zero or more more characters: `\/(.*)\/` The parentheses pull the actual date text out into a group.
3. But, there's still a problem with this. Notice that there was a match on the final row where there is no data, only the slashes with no date between. Instead let's use the `+` character, which matches one or more characters: `\/(.+)\/`
4. Now we're getting somewhere. But let's try to break out the parts of the date, like we did for the nice standardized dates. `\/(.+) (.+), (.+)\/`
5. Nearly there, but one date didn't match! It doesn't fit the pattern of the rest of the dates; there is no comma after the day. We can fix this by putting a `?` after the comma, making it optional: `\/(.+) (.+),? (.+)\/`
6. If you have keen eyes, you may have noticed there are a few typos in this dataset. For example, one line has the year '201'. Let's force the year part of the pattern to have four digits. One way to do this would be: `\/(.+) (.+),? (....)\/`. Another option is to use curly braces, which let you specify the number of times the match must occur: `\/(.+) (.+),? (.{4})\/`
7. While we're at it, lets enforce some rules for the days as well. There should only be one or two digits in a day. Curly braces can be used to specify a range in the number of matches: `\/(.+) (.{1,2}),? (.{4})\/`
8. What about that line that is missing the day though? Why does that match? Let's pick up this example again in the section on Character Sets, below.

### Greedy vs lazy quantifiers

* Quantifiers are greedy by default - they will match as much text as they possibly can. A good example is trying to match text within html or xml tags. For example copy the following text into Regex101: 

		Extract everything "within quotes" from "this sentence".

* Using `".+"` matches the entire text from the first quotation mark to the second. Use the question mark to make the expression lazy instead: `".+?"` 
* Another solution would be to require the expression to match anything that is not a quotation mark, using `^`. For example, `"[^"]+"` will match characters that are not quotation marks, and therefore will stop matching each time it gets to an ending quotation mark.
* Use grouping to pull out the text within the quotation marks: `"(.+?)"`
