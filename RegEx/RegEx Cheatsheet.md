___
## Table of Contents
1. [[RegEx Cheatsheet#Introduction|Introduction]]
2. [[RegEx Cheatsheet#Useful Descriptions|Useful Descriptions]]
3. [[RegEx Cheatsheet#You should knows|You Should Knows]]
4. [[RegEx Cheatsheet#References|References]]

## Introduction
***

>A regular expression is a sequence of characters that specifies a match pattern in text. Usually such patterns are used by string-searching algorithms for "find" or "find and replace" operations on strings, or for input validation.

\- Wikipedia Editor Team, https://en.wikipedia.org/wiki/Regular_expression
Likewise, all regular expressions can be chained.

Regular expression results are either matched, captured, or grouped. Matched meaning the match matches the regular expression by context. These can be either full or partial particularly in the literal meaning. Captured meaning the match matches the regular expression and is used to carry information to the end result. Grouped meaning matched and captured, but only within a certain context specifically using `()` to denote both groups and sub-groups. When you specify the groups, the context no longer automatically captures the entire regular expression instead each group is used as the capturing method.

## Useful Descriptions
***
Special Character | Description
--- | ---
\n | New line
\r | Carriage Return (older systems)
\t | Tab
\v | Vertical tab

Character Classes | Description
-- | --
\c | Control character
\s | Whitespaces
\S | Not whitespaces
\d | digits
\D | Not digits
\w | Word
\W | Not words
\x | Hexadecimal digits
\O | Octal digits

Anchors | Description
--|--
^ | Start at the beginning of the regular expression
$ | End at the end of the regular expression
\b | Word boundary
\B | Not word boundary
\\< | Start of word
\\> | End of word
\A | Start of string
\Z | End of string

Meta Characters | Description
--- | ---
. | Matches all non-carriage and non-newline characters
\\ | Escape both special and non-special characters

Quantifiers | Description
-- | --
\* | 0 or more
\+ | 1 or more
? | 0 or 1
{num} | Exactly num
{num,} | Exactly num or more
{,num} | Exactly num or less
{num1, num2} | Must be between num1 and num2

Expression | Use | Example | String | Result
--|--|--|--|--
Word | Matches all characters within the context | Foo | Foo | Foo
.\* | Matches the entire string with the meta character and quantifier recursively | .\* | foo bar | foo bar
word-word | Specify range of characters (specific context) | a-z+ | abcde12345po | \[abcde, po]
\^ | Matching the very start of the string | \^string | stringstringstring | string (index 0)
$ | Matching the very end of the string | string$ | stringstringstring | string (index 12)
^$ | Matching the very start of the string and end | \^string$ | stringstringstring |
\[] | Specify only the characters, classes, or ranges inside | \[abc]de | abcde | cde
\[^] | Specify all characters, classes, or ranges except inside | \[^abc] | abcde | de
() | Match and capture the expression inside the group | (foo)bar | foobarbarfoo | foobar
(()) | Match and capture the expression inside the group or sub-groups but capture both | (foo(bar)) | foobarbarfoo | \[foobar, bar, bar, foo] 
(?>) | Atomic group | (?>foo\|foot)s | foosfoots | foos 
(?:) | Non-capturing passive group | (?:foo)bar | foobarbarfoo | bar (index 3)
(?=) | Lookahead positive | A(?=B) | ABBA | AB
(?!) | Lookahead negative | A(?!B) | ABBA | A (index 0)
(?<=) | Lookbehind positive | (?<=B)A | ABBA | BA
(?<!) | Lookbehind negative | (?<\!B)A | ABBA | A (index 0) 
(\|) | Match and capture either or, also (?:\|) can be used in replacement for non-capturing groups | (cat\|dog) pet | catdog pet | dog pet 
\b | Matching the word boundary context | \b\w+ | this is where we stand | \[this, is, where, we, stand]
? | Optional match | ((?:cat\|dog)?pet) | catdogpetdogcatpetpet | \[dogpet, catpet, pet]
()?(?(1)\|) | Conditional expression | (hello)?(?(1) world\| bye) | something bye | bye
\\ | Match the escaped characters | \\\*pizza\\? | \*pizza? | \*pizza?

## You Should Knows
***
### Python Regular Expressions

In Python, you can start creating regular expressions by creating a raw string and importing the built-in regular expressions module

```python
import re

string = r""
```

From the module, there are three different types of ways to parse string information and each have their own use. `re.match(raw string, string)` matches the raw strings with the `^` character always at the beginning, hence its recommended to be used for quick match searches. `re.search(raw string, string)` searchs for the first known match without finding the alternatives or extras. `re.findall(raw string, string)` finds all matches associated with the raw string expression.

```python
string = "This is my final message, save the world, this is my farewell."
raw_string = r"is my final" # Get all 

re.match(raw_string, string) # []
re.search(raw_string, string) # "is my final"
re.findall(raw_string, string) # "["is my final", "is my final"]"
```

### Lookahead v.s. Conditional

To summarize, lookahead can be used when the context requires a if statement, while vice versa, conditional can be used when the context requires a if-else statement. Both can be used interchangeably when applicable.

## References
***
### Tools
[Great tool for testing realtime RegEx](https://regex101.com/)

### Resources
[Great intro for first starting out](https://regexone.com/)
[Another made cheatsheet for RegEx](https://cheatography.com/davechild/cheat-sheets/regular-expressions/)
[Great information on lookahead and atomic groups](https://stackoverflow.com/questions/2973436/regex-lookahead-lookbehind-and-atomic-groups)
[Extremely useful regex tutorial (also Novice to Advanced RegEx in Less-than 30 Minutes + Python by James Briggs), covers everything discussed](https://youtu.be/GyJtxd14DTc)