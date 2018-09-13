# Useful Regular Expressions
Created Sunday 26 August 2018

These are some of the most common regular expressions that we will encounter.
There are a few usage instructions, most importantly these are not 1 size fits all expressions

It depends on the requirements as regular expressions can be written broadly (permissive) or narrowly (restrictive, brittle)
Best example

### Regular expression: Match a date's year
``/\d{4}/ ``matches any year from 0000-9999 (broadest expression possible)
``/(19|20)\d\d/ `` matches 1900-2099
``/(19[5-9]/20[0-4])\d/`` matches 1950-2049

**Golden rule**: Never use someone else's regular expression without checking it carefully and fine-tuning it for your specific purpose.

Tips to write a regular expression

* Examine the data to be matched
* Determine what aspects of the data are important
* Determine what level of precision is required
* Make a list of "edge/corner cases" to test
	* Longest, shortest
	* Highest, lowest
	* Most unusual, most oddly formatted
* Use anchors, delimiters or context as ``/w+/ ``matches "#$%^__W__^&*(" so we can use other variations like '``/^w+$/``',`` '/\b\w+\b/``', '``/ \w+ /', `` '``/,\w+,/`` ' , '``/and \w+\./``'
* Be mindful of Greediness and Laziness


### Regular expression: Match names
simplist way is to use ``/\w+/ `` but as discussed before the word character only mates words and numbers and matches $__kevin__
``^([A-Z][A-Za-z.'\-]+) (?:([A-Z][A-Za-z.'\-]+) )?([A-Z][A-Za-z.'\-]+)$``
First Name				Middle name (non capturing)    Last name

This may not work for international name but and some exceptions are present so special cases need to be verified as well

### Regular expression: Postal codes
**US (five digits & 4 optional digits)**: ``^\d{5}(?:-\d{4})?``
**Canada (A9A 9A9)**: ``^[A-Z]\d[A-Z] \d[A-Z]\d$ ``
**UK (many possible formats available):**  ``^([A-Z]{1,2}\d{1,2}|[A-Z]{1,2}\d[A-Z]) \d[A-Z]{2}$``
*Check in wikipedia for UK postalcodes regex*

There can be some locations/zip coes that are not used/existing but since locations are evolving database will have new entries over time thus dont limit the regex as constant maintenance will be required.

### Regular expression: Email addresses
``^[\w.%+\-]+@[\w.\-]\.[A-Za-z]{2,6}$``
There are other domain names that we may not know
								

### Regular expression: URLs
Sample URL: *http:*www.nowhere.com*, *<http://nowhere.com/images/page.html//>, ...
``^(?:http|https|ftp):\/\/[\w.\-]+(\.[\w\-]+)+.*$``

### Regular expression: decimal numbers and currency
Be careful  as it may happen that everything is optional and the number as string problem will also appear
**Floating Number**: ``^(\d*\.\d+|\d+)$``
**Currency**: ``^(\$|\u00A3|\u00A5|\uFFE5)(\d*\.\d+|\d+)$``

### Regular expression: matching IP addresses
``^(([01]?[0-9][0-9]?|2[0-4][0-9]|25[0-5])\.)+([01]?[0-9][0-9]?|2[0-4][0-9]|25[0-5])$``

### Regular expression: matching dates
Format needs to be specified else it will be hard 
Format: *year,month,date*
``^\d{4}[\-/](0?[1-9]|1[0-2])[\-/](0?[1-9]|[12][0-9]|3[01])$``

### Regular expression: matching times
12 hr,24hr ,GMT -diff, EST|PST|IST
``^(([0-1]?[0-9]|2[0-3])(:[0-5][0-9])+( [A-Z]{3}( [-+]\d)?)?|(0?[1-9]|1[0-2])(:[0-5][0-9])+[AaPp][Mm])$``

### Regular expression: matching html tags
``/^<(?:([A-Za-z][A-Za-z0-9]*)\b[^>]*>(?:.*?)</\1>|[A-Za-z][A-Za-z0-9]*\b[^/>]*/>)$/m``

### Regular expression: matching passwords
``/^(?=.*\d)(?=.*[~!@#$%^&*()_\-+=|\\{}[\]:;<>?/])(?=.*[A-Z])(?=.*[a-z])\S{8,15}$/m``

### Regular expression: credit card numbers
``/^(?:3[47]\d{2}([\- ]?)\d{6}\1\d{5}|(?:4\d{3}|5[1-5]\d{2}|6011)([\- ]?)\d{4}\2\d{4}\2\d{4})$/m``

### Finding words near other words
``/\b[Aa]\b(?= (?:\w+[\- :;.]){0,5}\b[Mm]an\b)/``

### Formatting with Search and Replace
useful and done in gedit, notepad++

