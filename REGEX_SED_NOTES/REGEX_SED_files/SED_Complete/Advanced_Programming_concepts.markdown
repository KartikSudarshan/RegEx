# Advanced Programming concepts
Created Sunday 26 August 2018

``N,P,D`` 		↔  to manage multiline pattern space
``:,b,t`` 		↔  to manage program flow control
``g,G,h,H,x``	↔  to manage the hold buffer

### Managing Multiline pattern
N ⇒ appends a newline and reads in the next input line 
P ⇒ prints up to the first new line
D ⇒ Deletes up to and including the first new line
like d, D stops processing but doesn't get the next line unless it leaves the pattern space empty

### Managing program flow control
: ⇒ defines a label
b ⇒ branches to a label
t ⇒ branches only if any substitution have occured

### Managing the hold buffer
h ⇒ copies pattern space into the hold buffer
g ⇒ copies hold buffer into the pattern space
H ⇒ appends new line + copies pattern space into the hold buffer
G ⇒ appends new line + copies hold buffer into the pattern space
x ⇒ exchanges pattern space and the hold buffer


Script:
	/marched/ {
	N
	s/\n/ - /
	}


Script:
``N``
``s/marches.*up/marches...up/``
``P``
``D``

Script:	``s/the/THE/g``
	b next
	s/up/UP/g
	: next
	s/down/DOWN/g
	b
	s/marched/MARCHED/g
	

Script:
``s/again/again/``
``t label``
	s/the/The/h
	: label
	s/up/UP/g



Script:
	2{
	h
	}
	${
	p
	g
	}

Script:
	:top
	/_/ {
	x
	/ON/ ! {
	s/.*/ON/
	x
	s;_;<i>
	}
	/ON/  {
	s/.*/OFF/
	x
	s;_;</i>
		}
	b top
	}


