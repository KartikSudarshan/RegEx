# Grouping and Alternation Expression
Created Sunday 26 August 2018

Grouping Metacharacters
-----------------------
Grouping metacharacters are easiest metacharacters
| Metacharacter | Meaning                  |
|:-------------:|:-------------------------|
|       (       | Start grouped expression |
|       )       | End grouped expression   |


Group portions of the expression
- Apply repetition operators to a group
- Makes expressions easier to read
- captures group for use in matching and replacing
- cannot be used inside a character set

E.g.
``/(abc)+/ ``matches "__abc__" & "__abcabcabc__"
[/(in](file:///(in))?dependent/ matches "__independent__" & "__dependent__"

``/run(s)?/`` is the same as ``/runs?/``

Alternation Metacharacters
--------------------------
| Metacharacter | Meaning                           |
|:-------------:|:----------------------------------|
|      ∣      | Match previous or next expression |


'``|``' is an OR operator
- Either match expression on the left or match expression on the right
- Ordered, leftmost expression gets precedence
- Multiple choices can be daisy-chained
- Group alternation expression to keep them distinct

``/apple|orange/ ``matches "__apple__" and "__orange__"
``/abc|def|ghi|jkl/ ``matches "__abc__", "__def__", "__ghi__", "__jkl__"
``/apple(juice|sause)/ ``matches is not the same as ``/applejuice|sause/``
``/w(ei)|(ie)rd/ ``matches __weird__ and __wierd__

Writing logical and efficient alternations
------------------------------------------
Always remember:
**Regular expressions engines are eager. **
**Regular expressions engines are greedy. **

``/(peanut|peanutbutter)/`` match prefers peanut first in __peanut__butter
so ``/peanut(butter)?/ ``match prefers __peanutbutter__

It matches whatever it can when it has multiple matches
xyz|abc|def gives an match for abc in __abc__defghi 

Put simplest or most efficient expression first
e.g. Which is more efficient?
Regex1:  ``/\w+_\d{2,4}|\d{4}_\d{2}_\w+|export\d{2}/``

Regex2:  ``/export\d{2}|\d{4}_\d{2}_\w+|\w+_\d{2,4}/``

**Ans:** Regex2

Repeating and nesting Alternations
----------------------------------

Repeating Alternations is easy and possible
- First matched alternation does not effect the next matches
- ``/(AA|BB|CC){6}/`` matches "AABBAACCAABB"

Check Nesting carefully
-Best way is process it text deditor first then combine

e.g. 
``/(apple (juice|sauce)|milk(shake)?|sweet (peas|corn|potatoes))/``





