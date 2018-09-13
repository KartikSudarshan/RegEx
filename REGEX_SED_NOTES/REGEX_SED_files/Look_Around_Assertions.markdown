# Look Around Assertions
Created Sunday 26 August 2018

We will be learnig about the 2 main types:

1. Look Ahead 
2. Look behind 


Positive look ahead assertions
------------------------------
| Shorthand | Meaning                        |
|:---------:|:-------------------------------|
|    ?=     | Positive Look Ahead assertions |


This is used in a grouped expressionas the first character inside the parenthesis
Look ahead assertion is an assertion of what ought to be ahead
if look ahead assertion fails then whole match fails
Any valid regular expression can be used as an assertion
These assertions are zero width, does not include group in the match
	

### Support
Most modern regex engines except UNIX

### Syntax
``/(?=regex)/``

### Examples
``/(?=seashore)sea/ ``matches sea in __sea__shore but not seaside
This is similar to ``/sea(?=shore)/``

This only asserts but doesn't matches

Double testing with lookahead assertions
----------------------------------------
We saw that ``/(?=seashore)sea/ ``is similar to ``/sea(?=shore)/ `` but there is a difference in the order in which the expression is executed

``/(?=seashore)sea/ ``Assertion is attemted first then the sea match is attempted
``/sea(?=shore)/ ``The sea match is attempted then the  Assertion 

Order matters if [RegEx](./RegEx.markdown) is used for speed and efficiency.

The Second difference is the position where it starts looking for each expression
In first expression rewinding is done twice
In Second expression rewinding is done once

Thus first E.g. allows us to match a pattern that also matches another pattern
``/\d{3}-\d{3}-\d{4}/ `` matches 555-301-4321 & 123-456-7890
``/^[0-5\-]+$/ ``matches 555-301-4321 & 12346-5
So the above 2 expressions can be combined to 1 expression

``/(^[0-5\-]+$)\d{3}-\d{3}-\d{4}/ ``matches 555-301-4321
Now we can run 2 regex tests on the same string & can be cascaded
``/(^[0-5\-]+$)(?=.*4561)\d{3}-\d{3}-\d{4}/ ``matches 555-301-4321

Negative Look ahead assertions
------------------------------
| Shorthand | Meaning                        |
|:---------:|:-------------------------------|
|    ?!     | Negative Look Ahead assertions |


### Syntax
``/(?!regex)/``
! ↔ not this regualar expression thus it retruns opposite results

### Examples
``/(?!seashore)sea/ ``matches sea in __sea__side but not seashore
This is similar to ``/sea(?!shore)/``
 
Now way to tell when **not **to match for something. Negative lookahead assertions always help us  to do this


LookBehind assertions
---------------------
| Shorthand | Meaning                         |
|:---------:|:--------------------------------|
|    ?<=    | Positive Look Behind assertions |
|    ?<!    | Negative Look Behind assertions |


Assertion of what ought to be behind
Similar to look ahead assertions
if look ahead assertion fails then whole match fails
Any valid regular expression can be used as an assertion
These assertions are zero width, does not include group in the match
	
### Syntax
``/(?<=regex)/``
``/(?<!regex)/``

### Examples
``/(?<=baseball)ball/ ``matches ball in base__ball__ but not football
This is similar to ``/ball(?<=baseball)/ ``but normally first 1 is used for efficiency purpose

``/(?<!baseball)ball/ ``matches ball in foot__ball__ but not baseball
This is similar to ``/ball(?<!baseball)/ ``but normally first 1 is used for efficiency purpose

Main Difference in lookbehind expression is the Support

### Support
Simple expression in .NET, Java, Perl, PHP, Python, Ruby 1.9
Not supported in JavaScript, Ruby 1.8 and old Unix tools

Simple expressions mean fixed length so Literal text and character classes can be used but no repetition or optional expressions
alternation only with fixed length items (?<=cat|dog|rat) but  not (?<=apple|banana|plum)

use texteditor to test


The power of positions
----------------------
Allow testing of a regular expression  apart from matching
Peek forward/backward e.g. ``/sea(?=shore)/``
Match a string using multiple expressions
Define rejection strings
Find Last occurance of something

All assertions are zero width ↔ zero position movement
when ``/(?=seashore)sea/ ``asserts first then rewinds to matches sea in __sea__shore 
if you have 2 aasertions with no expression nothing gets  matched i.e. match exists but is zero width
Where is the regex pointer?
Useful for inserting text (find and replace)




