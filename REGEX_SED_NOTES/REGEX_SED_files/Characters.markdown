# Characters
Created Sunday 26 August 2018

Literal Characters
------------------
simply put 'a' matches 'a'. So we will be working with strings
``/car/`` matches "__car__"
``/car/`` matches "__car__nival" (like a word processor & the simplist match)

These searches are **case sensitive** by deault
``/car/`` doesn't match ``"Car"`` due to case sensitivity
``/Car/`` doesn't match ``"carnival"`` due to case sensitivity
``/car/`` doesn't match ``"c a r"`` as the words have spaces in between

Global is **not** default in RegEx so in Standard (non-global) matching earliest (leftmost) match is preferred
In Global matching, all matches are found throughout the text

#### Default:
``/zz/`` matches "pi__zz__azz" 

#### Global:
``/zz/`` matches "pi__zz__a__zz__" 

**Regular Expressions are eager**

Metacharacters:
---------------
A character that has special meaning

* like mathamatic operators
* Transform literal chracters into powerfil expressions
* Only few to learn ``\ . * + - { } ^ $ | ? ( ) : ! =``
* They can have more than 1 meaning
* Variations between regex Engines


The Wildcard Metacharacters
---------------------------
Dot ``.``↔ Any Character except newline  
since original unix regex tools were linebased
``/h.t/  ``matches "__hot__" "__hat"__ "__hit"__ "__hzt"__ "__h t"__ "__h:t"__ but does not match "heat" as dot is only for single character
Thus its the broadest match possile and mist common metacharacter used but also the modt common mistakes are made as well
``/9.00/  ``matches "__9.00__" , but also matches "__9500__" & "__9-00__"

The challenge in regular expressions is matching what you want and in matching only what you want
Dot matches all takes away the restriction of newline character (a feature added later)

Escaping Metacharacters
-----------------------
How to convert Dot  as a decimal point? Escape it by ``\.``
``/9\.00/  ``matches "__9.00__" , but doesn't matches "9500" & "9-00"

To escape ``\ `` use ``\\``
To escape ``/ `` use ``\/``
only metacharacters need to be escaped not literal characters as it gives them special meaning
``\d`` is different from ``d``
**Quotations are not metacharacters so no need to escape**

Other Special Characters
------------------------

* Spaces (use literal space "``\ ``")
* tabs (use ``\t``)
* Line Returns (``\r``, ``\n``, ``\r\n``) \r ↔ line return, \n ↔ newline
* Non printable characters
	* bell (``\a``)
	* escape (``\e``)
	* form feed (``\f``)
	* vertical tab (``\v``)
* ASCII and ANSI codes
	* Codes that control the appearence of the text terminal
	* ``0xA9`` ↔  ``\xA9``


