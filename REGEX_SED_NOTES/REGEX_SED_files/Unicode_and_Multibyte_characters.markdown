# Unicode and Multibyte characters
Created Sunday 26 August 2018

About unicode
-------------
If you live in a country those language consists of characters outside of the Roman alphabet,
characters beside simple a-z then this information is going to be essential

#### Single Byte:
Uses 1 byte (eight bits) to represent a character 2^8^=256 characters


#### Double Byte:
Uses 2 byte (16 bits) to represent a character 2^16^=65,536 characters

Still many other charactersLatin, Symbols ,other languages
So >109000 characters

### Unicode
variable byte size
maintains compatibility with one & 2 byte encoding
allowing for >1 million characters
Mapping between a character and a number
"U+" followed by a four-digit hexadecimal number
infinity sign is written as U+221E
Combinations can be done as well


Unicode in regular expressions
------------------------------
We can use unicode for matching lots of things,languages,symbols
But some issues are present:

* Words can be spelled in multiple ways
* Words can be encoded as four or five characters
* Wild card Matching
* Backtracking
* Unicode is relatively new


### How to handle these in regular expressions?
There is a uncode indicator: \u
\u followed by a 4 digit hexadecimal number (0000-FFFF)
so ``/caf\u00E9/`` matches a spelling of cafe but not "cafe"


### Support
Java,JavaScript, .NET, Python,Ruby
Perl, PHP support but use \x instead
Not supported in unix tools


Unicode wildcards and properties
--------------------------------
How to use wildcard with unicode?
1^st ^Solution: Unicode Wildcard \X
Matches anysingle characters regardless of coding
Always matches line breaks like (like [/./s)](file:///s))
``/caf\X/ ``matches multiple spellings of cafe

### Support
Only supported in Perl and PHP

2^nd ^Solution: Unicode Property \p{property}
Matches all characters that have this property
``/\p{Mark}/ ``or ``/\p{M}/ `` matches any mark (accents)
``/\p{Letter}/ ``or ``/\p{L}/ `` matches any letter 
Always matches line breaks like (like [/./s)](file:///s))
``/caf\X/ ``matches multiple spellings of cafe

| Unicode Property | Abbreviation |
|:----------------:|:-------------|
|      Letter      | L            |
|       Mark       | M            |
|    Seperator     | Z            |
|      Symbol      | S            |
|      Number      | N            |
|   Punctuation    | P            |
|      Other       | C            |


Unicode not-Property \P{property}
Matches characters that do not have a property
``/caf\P{M}\p{M}/`` matches 'cafe'


### Support
 Java .Net Perl PHP and Ruby 
Not javascript python and old unix tools
	


