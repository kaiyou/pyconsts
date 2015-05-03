pyconsts
========

Except for configuration-based constants that should be managed in
configuration files, one often has to declare module-specific constants when
writing code. For instance: one might plan on coding multiple choice values,
naming monkey-patched attributes or dynamic database fields.

Dictionaries are the most straightforward implementation. Object-like syntax is
however best suited for code readability and one should make sure these
constants are in fact constant (not modified during the course of the program).

Enum are also quite useful at achieving this goal, yet they lack the
immutability and their syntax is more suited for enumerating attributes than
storing constant values.

pyconsts aims at providing simple functions for constant management. Constants
are enforced during a single runtime. Therefore, one should not rely on
pyconsts for constants that must remain unchanged over the course of multiple
runtimes (protocol constants for instance).

Use cases
=========

Coding for enum-like indices
----------------------------

``` python
Colors = pyconsts.index(
  "red", "blue", "green"
)

color = Colors.red

if color == Colors.red:
  print "This is red!"

elif color == Colors.blue:
  print "This is blue instead!"
```

Naming attributes when monkey patching
--------------------------------------

``` python
ATTR = pyconsts.text(pattern="__monkey_%s__",
  "COUNT", "VALUE"
)

setattr(mypatchedtype, ATTR.COUNT, 2)
print(mypatchedtype.__monkey_COUNT__)
```
