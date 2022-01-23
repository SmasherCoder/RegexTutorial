# Regex Tutorial (Regex Tutorial)

This is a tutorial that will be taking a brief look into what Regex (regular expressions) are and how they work. I hope this tutorial will help you break down the different sections of a regex so that it makes more sense.

## Summary

Regex (short for regular expression) is a string of characters that allow you to create search patterns that manage, match, and locate text. An example code snippet of regex shows as following:
```
^(\+\d{1,2}\s)?\(?\d{3}\)?[\s.-]\d{3}[\s.-]\d{4}$
```
* A regex that used to match a phone number

Regular expressions can also be used from within text-editors to find text within a file and at the command line. 

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)

## Regex Components

### Anchors
Anchors are characters within the regex that allow you to match strings that begin with or ends with (or both) certain characters. 

Examples:
```
^Travis          matches any string starting with "Travis"
Helms$           matches any string ending with "Helms"
^Travis Helms$   matches the exact string
goodbye          matches the exact text "goodbye" in it
```

### Quantifiers
Qunatifiers are characters within the regex that tells you how many instances of a character, group, or character class can be represented in the string to be matched.

Examples:
```
cat*        matches a string ca followed by zero or more t
cat+        matches a string ca followed by one or more t
cat?        matches a string ca followed by zero or one t
cat{2}      matches a string ca followed by 2 t
cat{2,}     matches a string ca followed by 2 or more t
cat{2,5}    matches a string ca followed by 2 up to 5 t
c(at)*      matches a string c followed by zero or more copies of the sequence at
c(at){2,5}  matches a string c followed by 2 up to 5 copies of the sequence at
```

### OR Operator
OR Operators (Alternation Operator) matches on of a choice of regular expressions: if you put the character(s) representing the alternation operator between any two characters in the regex, the result matches the union of the strings that those two characters match.

Examples: 
```
c(a|t)  matches a string that has c followed by a or t (and captures a or t)
c[at]   matches a string that has c, but without capturing a or t
```

### Character Classes
Character Classes (Character Set) tells the regex engine to match only one out several specific characters, such as digits, words, or whitespace.

Examples:
```
\d    matches a single any digit 0-9
\w    matches a single any character that is a-z
\s    matches ` `
.     matches any character
\D    matches a single non-digit character
\W    matches a single any non-character that is a-z
\S    matches a single non-` `
```

### Flags
Flags are optional parameters that we can add to a plain expression to make it search in a different way. Each flag is denoted by a single alphabetic character, and serves different purposes in modifying the expression's searching behavior.

Examples:
```
/Travis/g   matches all "Travis" in the test
/Travis/m   matches the beginning and ending of each line with "Travis", rather than the whole string "Travis" itself
/Travis/i   matches all "travis" despite case (Travis, tRavis, tRAVIS, TRAVIS all match)
```

### Grouping and Capturing
Grouping allows for a pattern or string so that it is matched in a complete block.

Examples:
```
c(at)           parentheses create a capturing group with value at
c(?:at)*        using ?: we disable the capturing group
x(?<bar>yz)     using ?<bar> we put a name to the group
```

### Bracket Expressions
Bracket Expressions are characters enclosed by a bracket `[]` matching any single character within the brackets. 
*note: if the first character within the brackets is a `^` then it signifies any chracter **not** in the list, and is unspecified whether it matches an encoding error. 
tion of expression)

Examples:
```
[cat]         matches a string that etiher has c or c a or c t (same as c|a|t)
[c-a]         similar to case above
[u-zU-Z0-9]   a string that represents a single hexadecimal digit, case insensitively
[0-9]%        a string that has a character from 0-9 before a %
[^a-zA-Z]     a string that has not a letter from a to z or from A to Z
```

### Greedy and Lazy Match
Greedy and/or Lazy Matching are quantifiers that expand the match as far as possible through the text. 

Examples:
```
<.+?>     matches any character that is one or more times included inside `<` and `>`, and expands as needed.
<[^<>]+>  matches any character expects `<` or `>` one or more times included inside `<` and `>`. 
```

### Boundaries
Boundaries are the places between characters. A Boundary should be thought of as a wall between any adjacent characters.
There are two types of Boundaries, **Word** and ***Non-Word**, each denoted by a specific character. 

Examples of Boundaries are as follows:
```
`Travis Helms` has 13 total Boundaries with 8 Word Boundaries as seen below:
|T|r|a|v|i|s| |H|e|l|m|s|
^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^
N W W W W W N N W W W W N -  N = Nonword Boundary \ W = Word Boundary
\bcat\b     matches a "whole words only search" for the string "cat"
\Bxyz\B     matches only if the pattern is fully surrounded by word characters `txyzt` would match the string `xyz` because it only has word boundaries
```

### Back-references
When using Grouping (look above) you may Capture the Group, which is saved in memory for later use. Backreferencing is the name given to the action of using these matches. 
Backreferencing is the refernce of a captured match, save in memory, by a captured group.

Examples are a follows:
```
([xyz])\1              using \1 it matches the same text that was matched by the first capturing group
([uwx])([yz])\2\1      we can use \2 (\3, \4, etc.) to identify the same text that was matched by the second (third, fourth, etc.) capturing group
(?<bar>[xzy])\k<bar>   we put the name bar to the group and we reference it later (\k<foo>). The result is the same of the first regex
```
### Look-ahead and Look-behind
Look-ahead and Look-behind (lookaround) are `start and end` zero-length assertions [Anchors](#anchors) but they actually match characters, then ends the match, returning only the result: **Match or No Match**. They do not cosume characters in the string, but only assert wether a match is possible or not. Lookaround allows you to create regular expressions that are impossible to create without them, or that would get very longwinded without them.

Examples of Look-ahead and Look-behind are as follows:
```
h(?=t)       matches a h only if is followed by t, but t will not be part of the match
(?<=t)h      matches a h only if is preceded by an t, but t will not be part of the match

NEGATION OPERATOR

h(?!t)       matches a h only if is not followed by t, but t will not be part of the match
(?<!t)h      matches a h only if is not preceded by an t, but t will not be part of the match

```

## Author

Hi, my name is Travis Helms and I am a bootcamp student that is being taught by University of Texas of Austin.

Feel free to check out my GitHub repo for all of my previous and current projects that I am working on.

[GitHub Profile](https://github.com/SmasherCoder)