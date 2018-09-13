# Capturing Groups and back references
Created Sunday 26 August 2018

Backreferences
--------------
Grouped expressions are captured by the [RegEx](./RegEx.markdown) Engine. So as the regex engine is going through and finding matches it stores the matched portion that's in parentheses. 
E.g. 
``/a(p{2}l)e/ ``matches "apple" and stores "ppl"
Stored the data matched, not the expression
It is done automatically, by default (it doesn't matter if the parenthesis was used for other reasons like repetition, alternation, or keeping Regex organised)
If regex sees a match in the parenthesis it catures the data for later
Backreferences are used to acces the captured data
- Refer to the First backreference with \1
| Metacharacter | Meaning                              |
|:-------------:|:-------------------------------------|
| \1 through \9 | Back References for positions 1 to 9 |

2 ways to use back references

1. Can be used in the same expression as the group
2. Can be accessed after match is complete (in text editor or in programming language)
3. cannot be used inside character class


Most regex support \1 through \9. Some support  \11 through \99 (not much preferred).
Some regex engines use $1 through $9

``/(apples) to \1/ `` matches "apples to apples"
``/(ab)(cd)(ef)\3\2\1/ `` matches "abcdefefcdab"
``/<(i|em)>.+?</\1>/ ``matches "<i>Hello</i>" and "<em>Hello</em>"

It is the literal text that got matched not the expressions


Backreferences to optional expressions
--------------------------------------
Lets look into a special case where back reference refer to optional expressions

### Optional Elements
given a Regex ``/A?B/`` matches AB and B
Using back references on the above regex, the following occur

#### Captures occur on zero-width matches
When`` /(A?)B/`` matches "AB" and Captures A
When ``/(A?)B/`` matches "B" and Captures "" here it matches zero-width

#### Thus back references become zero width too
``/(A?)B\1/ ``matches "ABA" and "B"
``/(A?)B\1C/ ``matches "ABAC" and "BC"

#### Captures do not always occur on optional groups
When`` /(A)?B/`` matches "AB" and Captures A
When ``/(A)?B/`` matches "B" and Captures nothing as A was not optional. A was required eventhough group was optional

#### Thus back references is to a group that failed to match
``/(A)?B\1/ ``matches "ABA" but not  "B"
This is true in every regex engine Except Javascript

To review
Element is optional, group/capture is not optional
``/(A?)B/ ``matches B and captures ""

Element is not optional, group/capture is  optional
``/(A)?B/ ``matches B and captures nothing

Finding and replacing backreferences
------------------------------------
This done using text editor or programming language using the us_presedents file
Finding Regex: ``^(\d{1,2}),([\w .]+?) ([\w ]+?),(\d{4})``
Replacing Regex: ``\1 \3 \2 \4``

### Best way to use regex in Text Editor
Create a regular expression that matches the target data
Test the regular expression and revise as needed

* Use anchors and specifically to narrow scope

Add Capturing groups

* Capture anything that varies row-to-row

Write the replacement String

* Use all captures
* Add back anything not captured but still needed
* May need to use $1 instead of \1 in some text editors


Non capturing group expressions
-------------------------------
When parenthesis is added to an expression it gets captured by default. How to turn off this default behaviour?

| Metacharacter | Meaning                       |
|:-------------:|:------------------------------|
|      ?:       | Specify a non-capturing group |


### Syntax

* ``/(\w+)/ ``transforms to ``/(?:\w+)/``

Turn off the capture and back references

* Optimize for speed
* Preserve space for more captures most ony have 9 back refernces


### Supprt
Most regex engines except older unix tools

``/(:?regex)/ ``
here 
'?' = Give this group a different meaning
':' = The meaning is non-capturing


