# Character Sets
Created Sunday 26 August 2018

Defining character set
----------------------
Wild card character is also a character set that matches all characters or its a character set of all characters
This results to really broad matches.So now we narrow the expression

| Shorthand | Meaning               |
|:---------:|:----------------------|
|     [     | Begin a character set |
|     ]     | End a character set   |


Match any one of several characters (but only 1). Order of characters does not matter.
``/[aeiou]/`` matches only 1 vowel
``/gr[ae]y/`` matches "__gray__" & "__grey__"
``/gr[ae]t/`` does not match "great" but ``/gr[ae][ae]t/``  matches "__great__","__greet__","__graat__","__graet__"

Character Ranges
----------------
character ranges give a short cut to all the range of characters
| Shorthand | Meaning             |
|:---------:|:--------------------|
|     -     | Range of characters |

 
All characters between 2 characters Insode the Character set '``[ ]``' only its a metachatacter else it is a normal character
[0-9],[3-9], [5-7]
[a-zA-Z], [a-ek-ou-y]
for numbers say 50-99 dont use [50-99] it means 5,0-9,9. This is not math so proper way is [5-9][0-9]

Negative character sets
-----------------------
| Shorthand | Meaning                |
|:----------|:-----------------------|
| ^         | Negate a character set |


Not any one of the several charcters
Add ^ as the first character inside a charcter set. Still represents 1 character 

``/[^aeiou]/`` matches only 1 consonent
``/[^aeiou]/`` matches "__seek__" & "__sees__" & "__see__ "  but not "seem" & "seen" & "see"

Metacharacters inside character sets
------------------------------------
Metacharacters inside a character set are already escaped. so no need to escape them again
Some exceptions are ``] - ^ \``

``/var[[(][0-9][\])]/`` matches __var(1)__ __var[2]__
``file[0\-\\_]1 ``matches file01 file-1 file\1 file_1
sometimes escaping is not required 

### Shorthand character sets
All shorthand charactersets beginn with \ followed by a letter
| Shorthand | Meaning            | Equivalent    |
|:----------|:-------------------|:--------------|
| \d        | Digit              | [0-9]         |
| \w        | Word character     | [a-zA-Z0-9_]  |
| \s        | Whitespace         | [ \t\r \ n]   |
| \D        | Not a Digit        | [^0-9]        |
| \W        | Not word character | [^a-zA-Z0-9_] |
| \S        | Not a whitespace   | [^  \t \r\ n] |

	
'``_``' is a word character but '``-``' is not a word characterits considered a punctuation
``/\d\d\d\d/`` matches 1984 but not text
``/\w\w\w/`` matches ABC 123 and 1_A 
``/\w\s\w\w/`` matches  'I am' but not 'am I'

we can do mix and match in character set as well
Support is in PERL all modern regex engines and not many unix tools

Posix bracket expression
------------------------
POSIX standard came up with bracket expressions that would help define sets of characters
Similar to character sets in shorthand but slightly different

| Class      | Meaning                            | Equivalent |
|:-----------|:-----------------------------------|:-----------|
| [:alpha:]  | Alphabetic characters              | A-Za-z     |
| [:digit:]  | Numeric Characters                 | 0-9        |
| [:alnum:]  | Alpha Numeric characters           | A-Za-z0-9  |
| [:lower:]  | Lowercase Alphabetic characters    | a-z        |
| [:upper:]  | Uppercase Alphabetic characters    | A-Z        |
| [:punct:]  | Punctuation characters             |            |
| [:space:]  | Space characters                   | \s         |
| [:blank:]  | Blank characters (space, tab)      |            |
| [:print:]  | Printable Characters, spaces       |            |
| [:graph:]  | Printable Characters, no spaces    |            |
| [:cntrl:]  | Control Characters (non printable) |            |
| [:xdigit:] | Hexadecimal characters             | A-Fa-f0-9  |


We use this in a character class e.g. ``[[:alpha:]] [^[:alpha:]]``
Never try to mix and match Posix with shorthand
It can be used in Perl, PHP, Ruby, Unix
Java,JavaScript,Python dont support this


