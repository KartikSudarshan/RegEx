# Command Line Basics
Created Sunday 26 August 2018

The Most Basic Command Line Utility in SED. SED is always case sensitive
``"s/old/new/"``
replaces ``old`` with ``new`` 

##### Simply replace the to The in dukeof york.text
``sed 's/the/The/' ../dukeofyork.txt`` 

Note: Only first occurance was replaced in each line

##### Also SED does not edit the original input file unless it is given -i flag or > to other file
sed 's/the/The/' ../dukeofyork.txt >new1.txt
sed 's/men/women/' ../dukeofyork.txt

The removes ``"them" ``from duke of york
sed 's/them//' ../dukeofyork.txt

if Multiple Files are given, they are read in order
sed 's/the/The/' ../dukeofyork.txt ../array.c 

If file is not mentioned it processes standard input
sed 's/the/The/'

##### Other way to specify input/output is

sed 's/the/THE/' <../dukeofyork.txt 
sed 's/the/THE/' <../dukeofyork.txt >new2.txt
sed s/the/THE/  

Note: Quoting is not required in SED but it is preffered

sed 's/the/some of the/' <../dukeofyork.txt 
sed 's/thousand/$1000/' <../dukeofyork.txt 

if quotes are not given  then the substitution of $1 will be taken thus it becomes empty
sed s/thousand/$1000/ <../dukeofyork.txt 

sed "s/ten thousand men /$10000/" <../dukeofyork.txt 
Similar issue as '$1' was again empty

sed "s/were/weren't/" <../dukeofyork.txt 

##### To escape $
sed "s/were/\$weren't/" <../dukeofyork.txt 
sed "s/were/\$weren't really/" <../dukeofyork.txt 

##### For Repitative Patterns:
echo use g to affect every occurance in the line and its not recursive so g only affects input not output

SED replaces the pattern as soon as there is a match
sed s/aba/---/g
sed s/aa/a-a/g
echo "as seen it is not useful if pattern is overlapping"
sed "s/they/and they/" <../dukeofyork.txt 

