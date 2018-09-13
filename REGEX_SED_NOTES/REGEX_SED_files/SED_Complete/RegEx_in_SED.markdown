# RegEx in SED
Created Sunday 26 August 2018

'``s/old/new``' is similar to Regular Expressions
Please review [RegEx](./RegEx.markdown) 

^ ↔ Begins with
$ ↔ Ends with

/^abc/  matches __abc__d, __abc__de
/abc$/  matches d__abc__, wqs__abc__


* ☐ any character in the set (Character class)

range in character set[a-zA-Z0-9], [A-H],[0-9]
[^a-z] ↔ anything that does not start with a-z

"*" ↔ matches zero or more ('*' is greedy i.e. it can match as many characters as it possibly can e.g. matching tags in html via sed)
"+" ↔ matches one or more
"( )" ↔ repeats multiple times
/ab*c/ matches "__abbbbbbbbbbc__d"
/(ab)*c/  matches "__abababababababababc__d"

### Special Replacement Strings
& ↔ is replaced by what ever text was found

sed -e "s/the/(&)/"
``the`` is replaced by ``(the)``

here n is a number
\n is replaced the text found for the nth \(..\)
``sed -e "s/\(they\) \(were\)/\2 \1/"``
Replaces ``they were`` to ``were they``
``sed -e "s/were \([a-z]*\)/\1ed/"``
``were up ``to ``uped``
``were down`` to ``downed``

