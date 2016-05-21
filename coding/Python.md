# PYTHON

Math
----

Exponents: `eight = 2 ** 3`  
Modulo (returns the remainder from a division): `3 % 2` will return `1`.

String Formatting, Console output
---------------------------------
```
name = raw_input("What is your name?")
quest = raw_input("What is your quest?")
color = raw_input("What is your favorite color?")

print "Ah, so your name is %s, your quest is %s, " \
"and your favorite color is %s." % (name, quest, color)
```


`len("Charlie")` - returns the length of the string  
`"Delta".upper()` - returns uppercase  
`"Echo".lower()` - returns lowercase  
`str(3.14)` - converts number to a string  


datetime.now() prints current time and date (requires from datetime import datetime)


Boolean
-------

```
     Boolean Operators
------------------------      True and True is True
True and False is False
False and True is False
False and False is False

True or True is True
True or False is True
False or True is True
False or False is False

Not True is False
Not False is True

```

`not` is evaluated first, `and` is evaluated next, `or` is evaluated last.
