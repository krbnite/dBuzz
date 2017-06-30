## List of Commands
The simplest python program consists of a list of commands in a text file.
You can run such a program from the command line.

```python
occupation = 'astronaut'
thing = 'star';  face = ':-p'
one=1; two=2; three=3
print("Hello World!")
print("I'm an %s!" % occupation)
print("I am not a %s %s" % (thing,face))
print("If I add %d and %d, I get %d" % (
  one, two, three))
hilarious=False
joke_eval = "Isn't that joke so funny?! %r"
print(joke_eval % hilarious)
formatter = "%r %r %r %r"
print(formatter % (1,2,3,4))
print(formatter % ('one','two','three','four'))
print(formatter % (True,False,True,False))
print(formatter % (formatter,formatter,formatter,formatter) %\
  (1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16))
qry = """
SELECT var1,
  var2,
  var3
FROM my_table
  WHERE var1 > var2
"""
print(qry)
a = 'oh\nyea'
print('%s' % a) # interpreted string
print('%r' % a) # literal string
# Exit vim: <esc> :wq
# back at bash command line
python ex1.py
```

## Format characters

| Format Symbol | Conversion  |
----------------|-------------|
| %c | character |
| %s | string; use for display (%r for debugging) |
| %d | signed decimal integer |
| %e | exponential notation |
| %f | floating point number |
| %g | the shorter of %f and %e |
| %r | string literal (raw representation); use for debugging |

There are a [few others](https://www.tutorialspoint.com/python/python_strings.htm)... 

## Interactive Script
Note: 
* python2: raw_input()
* python3: input()

```python
age = input("How old are you? (in years)")
height = input("How tall are you? (in inches)")
print("You are %r years old and %r inches tall." %\
  (age,height))
```

## Getting help from the Bash shell
```
pydoc os
pydoc sys
```

## More interactivity
```python
from sys import argv
script, first, second = argv
print("The script is called", script)
print("The first argument is:",first)
print("The second argument is:",second)
input("Did you want to add a third argument? ")
```

---------------------------------------------

Left off at Exercise 14:
https://learnpythonthehardway.org/book/ex14.html




