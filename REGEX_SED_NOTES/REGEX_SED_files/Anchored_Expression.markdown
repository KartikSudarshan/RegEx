# Anchored Expression
Created Sunday 26 August 2018

Start and end anchors
---------------------
| Metacharacter | Meaning                            |
|:-------------:|:-----------------------------------|
|       ^       | Start of string/line               |
|       $       | End of string/line                 |
|      \A       | Start of String, never end of line |
|      \Z       | End of String, never end of line   |


Anchors reference a position, not an actual character
- Zero-width
 ``/^apple/ ``or ``/\Aapple/``
 ``/apple$/ ``or ``/apple\Z/``
 ``/^apple$/ ``or ``/\Aapple\Z/``

### Support
``^`` and ``$ ``are supported in all regex engines
``\A`` and ``\Z ``are supported in Java, .NET, Perl, Python, Ruby


Line Breaks and Multiline mode
------------------------------

### Single line mode
By Default Regular expressions use Single-Line mode
so ``^`` and ``$`` do not match line Breakes similarly ``\A`` and ``\Z`` do not match any Line Breaks
Many UNIX tools use single-line mode only

### Multiline Mode
There is lots of utility in using Multi-line mode
^ and $ will match at the start and end of the line
\A and \Z do not match at line breaks
Most Languages offer Multi-line option 
(Look into google for Multi line function for programming language)

Word boundries
--------------
| Metacharacter | Meaning                          |
|:-------------:|:---------------------------------|
|      \b       | Word Boundry (Start/End of Word) |
|      \B       | Not a word boundry               |


They reference a position not an actual character

### Conditions for matching

* Before the first word character in the string
* After a word character and a non-word character
* Between a word character and a non word character


**Word Characters** : [A-Za-z0-9_] or \w

### Support
Most Regex engines, but not in Early UNIX tools (BRE) 

e.g.
``/\b\w+\b/ `` finds 4 matches in "__This__ __is__ __a__ __test__" and "__abc_123__" as a whole but only part of "top-notch"

``/\BThis/`` does not match "This is a test"
``/\B\w+\B/ ``finds 2 matches in T__hi__s is a t__es__t 

sometimes it is efficient to add boundries to get the match (a lot of back tracking gets skipped)

Caution
space is not a word boundry
Word Boundry references a position
- not an actual character
- zero length

E.g.
apples and oranges

``/apples\band\boranges/ `` does not match
so proper match is 
``/apples\b \band\b \boranges/``

