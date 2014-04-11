# All Your Ducks in a Row #

## Data Structures in Python ##

What Your Computer Does While You Wait - Gustavo Duarte
How misaligning Data Can INcrease Performance 12x - Dan Luu

Python can import Struct

*  from struct import pack, unpack
*  Useful for interacting with C programs, usually for only low-level ops

Python also exposes Array (low level)

*  Arrays have all items of same type
*  Access element by start + size*index
*  from array import array
*  Good for C Libraries and I/O
*  PYthon has a number of specialized arrays

NumPy uses the base types for speed, because Python will create > n float
objects for sum([<float>]).
Normally Python will have to create a `float` object for each float it pulls
out of the array so that these can be represented to the users.

PyPy is smart enough to optimize an array of all of one type to a fast-dict

Python wraps everything because it needs to be able allow arrays to contain
many different data types

## Tuples ##

Tuples store arrays of addresses, uses indirection to prevent issues with
addressing an index. In fact, all Python Data Structures use this type of
indirection (address location instead of raw data)

Tuples are read-only and can do bounds checking because it knows its limits

## Lists ##

Lists only hold length, size of storage, and the address of the addresses of
the data in the list.

Lists amoritize additions, allocate more space needed at the end of the newly
copied list. This first copy takes a bit of time, but is saved over the rest of
the additions later.

Popping off the front of a list is very slow because Python has to readdress
every single item in the list (just like in js), popping off the end isn't a
problem because it's built for that

## Dict ##

PyCon 2010 The Mighty Dictionary Talk is good here

Dict grows by 2x or 4x it's size to amoritize its size
Resizes at 2/3 full
Only every 1/3-2/3 full, giving into the speed vs space tradeoff
Dict operations are fast and therefore good for new programmers

defaultdict handles non-existing keys by filling in missing with a 'default'
type

Compound dict keys can be built with a tuple, pretty neat
frozenset is good for keys that are unordered

Dicts always iterate in arbitrary order (unlike lists)
OrderedDict (from collections) good for things where you want ordered data, but
quick access

## Classes ##

__slots__ will allow you to more efficiently store/access your data

## Fetching a Range ##

bisect is great for snagging items from the middle

deque allows you modifies both ends of the item, great for queues (secretly
behind queue, but has a lock)

## Popularity Contest ##

heapq lest you fetch top n items of t in linear time, gives you `nlargest and
`nsmallest` to avoid sorting

Research:

  *  Priority Queue
  *  sched.scheduler
  *  Trees (good for tree-shaped data, not so important when everything is an
     object)


The Clean Architecture in Python 2013 PyCon Talk
