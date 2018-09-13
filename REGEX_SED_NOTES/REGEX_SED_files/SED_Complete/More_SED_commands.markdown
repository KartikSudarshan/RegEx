# More SED commands
Created Sunday 26 August 2018

Addresses can precede command (affect only certain lines). this can be done by

* Line number
* $ specifies the end of file
* ``/.../ `` specifies lines matching regular expression
* , specifies range of addresses (most commands)
* ! specifies range of addresses not matching address (most commands)


Later we will be using specific commands
p ↔ prints the specific lines
d ↔ deletes the specific lines
r ↔ reads a file at the specified line
w ↔ writes the specified line to a file
y  ↔ transforms characters like the tr command 
Y command does not help specify range or specify range of addresses

e.g. 
``sed '3s/up/UP/' ../dukeofyork.txt``
``sed -n -e "1,3p" ../dukeofyork.txt``
``sed -n  "/marched/,/when/p" ../dukeofyork.txt``

to reverse affect of cmd by preceding with !
``sed -n  '1,3!p' ../dukeofyork.txt``

``sed -n -e "1,3d" ../dukeofyork.txt``
``sed -n  '1,3!d' ../dukeofyork.txt``
``sed -e 's/up/UP/w writeFileUp' ../dukeofyork.txt``

Order matters when executing multiple statements

### Commands that affect multiple or entire lines
a ↔ append line after the line
i ↔ inserts lines before the line
c ↔ changes/replaces lines



