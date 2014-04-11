## Python Decorators ##

[Slides](http://files.basepi.net/talks/decorators/decorators-pycon-2014.pdf)

## What is a decorator? ##

They Wrap Functions

*  Add functionality
*  Modify behavior
*  Perform Setup/Teardown (like testing/db conns)
*  Diagnostics

## What is a Function? ##

Everything is an object in Python, functions are Objects
Closures are the same as JS for the most part, so you can have a function
constructor that maintains scope and returns a new function (factory pattern)

Decorators are also Closures (can also be created with Classes, well should be)

## Decorator is a bit of Syntactic Sugar ##

```python
@my_decorator
def myfunc = ():
  pass
```

translates to:

```python
def myfunc = ():
  pass
myfunc = my_decorator(myfunc)
```

## Versatile Decorators ##

Want more generic decorators so that the functionality can be re-used easily

`(*args, **kwargs)` can replicate any normal function call

```python
def inner(*args, **kwargs):
  return wrapped(*args, **kwargs)
```

## Problems with this style of Decorator ##

`__name__` will return "inner"
`ArgSpec` will not be useful

To fix this, Graham Dumpleton created wrapt

[Initial Blog Post](http://bitl.ly/decorators2014)

What about decorators w/o arguments?
`@unittest.skipIf()`

## How to use Wrapt ##

use the wrapt decorator around your decorator

## Good uses of decorators ##

*  Number of times function was called
*  Timing Code (mark start time, run function, then mark down completion time)
