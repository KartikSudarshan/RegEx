# Programs in SED
Created Sunday 26 August 2018

Sed Features we can use in scripts like
{...} 	↔ 	to group commands into blocks
n 		↔  	to get the next line 
q 		↔  	to exit the program (similar to break)
d 		↔  	terminates execution for current line (similar to break)
# 		↔ 	introduces a comment
= and l 	↔ 	are used for 

``sed -e 's/up/UP/' -e "s/down/DOWN/"`` can be written as follows

⇒ cat >script
	s/up/UP/
	s/down/DOWN/

⇒ cat >script
	/when/ s/up/UP/
	/when/ s/down/DOWN/

but it becomes tedious if multiple changes to be done so use ``{} ``so that it will be easy
⇒ cat >script
	/when/ {
	s/up/UP/
	s/down/DOWN/
``}``
⇒ cat >script
	/when/ ! {
	s/up/UP/
	s/down/DOWN/
``}``

This can be nested as well
⇒ cat >script
	3,6  {
	/when/ ! {
	s/up/UP/
``}``
	s/down/DOWN/
``}``

⇒ cat >script
	/marched/  {
	n
	s/^/((
	n
	s/$/))
``}``
⇒ cat >script
	/marched/  {
	n
	s/^/((/
	n
	s/$/))/
	q
``}``

⇒ cat >script
	/up/  {
	s/up/UP/
	d
	s/^/==/
``}``

⇒ cat >script
``# this is comment line``
	/up/  {
	=
	s/up/UP/
	=
	s/^/==/
``}``

⇒ cat >script
	s/ /	/3
	l

