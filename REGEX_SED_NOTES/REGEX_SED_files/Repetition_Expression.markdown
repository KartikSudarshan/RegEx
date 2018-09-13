# Repetition Expression
Created Sunday 26 August 2018

Repetition metacharacters
-------------------------
| Metacharacter | Item must exist | Meaning                        |
|:-------------:|:---------------:|:-------------------------------|
|       *       |  not required   | Preceding item 0 or more times |
|       +       |       Yes       | Preceding item 1 or more times |
|       ?       |  Not required   | Preceding item 0 or 1 time     |

	
Preceding item can be literal character short hand character set or even mre complicated expression

so ``/apples*/ ``matches "__apple__", "__apples__", "__applesssss__"
so ``/apples+/ ``matches  "__apples__", "__applesssss__" but not "apple" as '``s``' has to be present atleast once
so ``/apples?/ ``matches  "__apple__", "__apples__",  but not "__applesssss__" as '``s``' has to be repleated atmost once

``/\d\d\d\d*/``  or ``/\d\d\d+/`` matches 3 numbers or more (2nd method is preferred)

``/colou?r/`` matches "__colour__" & "__color__"

### Support
Supported in all Regex Engines
``+`` & ``? ``are not supported in BRE's (i.e. old Unix Programs like grep)

Quantified reptition
--------------------
'``*``' & '``+``' allow for unlimitted amount of repetition. Now if we need more precesion  use Quantified Metacharacters
| Metacharacter | Meaning                                             |
|:-------------:|:----------------------------------------------------|
|       {       | Start Quantified repetition of preceding characters |
|       }       | End Quantified repetition of preceding characters   |

working is similar to ``+`` and ``*``
``{min,max}``: **min** must always be included so it can be zero, **max** is optional

``\d{4,8}`` matches numbers with 4 to 8 digits
``\d{4}`` matches numbers with exactly 4 digits (min = max)
``\d{4,}`` matches numbers with 4 or more digits (max = infinite)

``\d{0,}`` is equivalent to ``\d*``
``\d{1,}`` is equivalent to ``\d+``

``/\d{3}-\d{3}-\d{4}/`` matches most U.S. phone numbers
``/A{1,2} bonds/ ``matches "__A bonds__","__AA bonds__" , "A__AA bonds__"

Greedy expressions
------------------
Important principle on how regular expressions work (Greedy expressions)
Often [RegEx](./RegEx.markdown) exgine will make  a choice on what to return as a match
Greedy is just a term to express how the [RegEx](./RegEx.markdown) engine make the choice by default

E.g. what is the result of ``\d+\w+\d+ `` on '01_FY_07_report_99.xls'
what is the result of ``".+", ".+" ``on "Milton", "Waddams", "Initech, Inc"
(use RegExPal and see the answer)

Standard repetition quantifiers are greedy
( The repetition quantified ) Expression tries to match the longest possible string
It will still differ to achieveing an overall match:

1. ``/.+\.jpg/`` matches "finename.jpg'
2. The + is greedy but gives back the ".jpg" to make the match
3. think of it is rewinding or backtracking

Gives back as little as possible
e.g.  ``/.*[0-9]+/ ``matches "Page 226"
here ``/.*/ ``matches "Page 26" while ``/[0-9]+/`` matches "6"

**Regular expressions engines are eager. **(Its eager to give a result)
**Regular expressions engines are greedy. **

Lazy Expressions
----------------
Can we make [RegEx](./RegEx.markdown) Engine make a different set of choices? Yes but we need to use meta character
| Metacharacter | Meaning                        |
|:-------------:|:-------------------------------|
|       ?       | Make Preceding Quantifier lazy |


### Synatx

* ``*? ``(lazy *)
* ``+? ``(lazy +)
* ``{min,max}?``
* ``??``


Instructs quantifier to use a "lazy strategy" for making choices

#### Greedy Strategy
Match as much possible before giving control to the next expression part

#### Lazy Strategy
Match as little as possible before giving control to the next expression part

* Still defers to overall match
* not necessarily faster or slower bit matches will be different (different strategy of starting the search)


##### Examples
``/\w*?\d{3}/``
``/[A-Za-z-]+?\./``
``/.{4,8}?_.{4,8}/``
``/apples??/`` 
first ``?`` tells that s repeats 0 or 1 time (since default is greed it will prefer 1 time i.e. apples)
second ``?`` tells that the search process is lazy so prefer apple (thus ``s`` is meaningless)
e.g.  ``/.*?[0-9]+/ ``matches "Page 226"
here ``/.*?/ ``matches "Page " while ``/[0-9]+/`` matches "266"

e.g.  ``/.*?[0-9]+/ ``matches Nothing as everything was optional

``\d+\w+?\d+`` matches only __01_FY_07___report_99.xls
``".+?", ".+?"``  matches only __"Milton", "Waddams"__, "Initech, Inc"

So different search strategies yeild different results

### Support
Most Regular Expressions **support this lazy quantifier** but Unix tools (BRE,ERE) **are always greedy** so not supported

Using repetitions efficiently
-----------------------------
If efficiency is not implemented in RegEx Pattern the search becomes inefficient as a lot of backtracking is done

Using either Greedy or Lazy Strategy doesn't imply that result will be obtained faster. S switching from Greedy to Lazy only switches the priority of searching.
How to make Regex efficient?

**Basic Rule:**
Efficient matching + less back tracking = speedy Results

Define the quantity of repeated expressions
``/.+/`` is faster than ``/.*/``
``/.{5}/`` and ``/{3,7}/`` is even faster
	
Narrow the scope of the repeated expression
``/.+/`` can transform to ``/[a-zA-Z]+/``
Provide clearer starting and ending Points
``/<.+>/`` can transform to ``/<[^>]+>/ ``for html tags
use anchors and word boundries as well
	
##### Examples
``/\w*s/``-----(imporoved)---->``/\w+s/``-----(imporoved)---->``/[a-zA-Z]+s/`` 

-----(imporoved)---->``/[a-z]+s/``
OR
-----(imporoved)---->``/[A-Z][a-z]+s/``

or search for whole words only 
Spaces, anchors or word boundries


