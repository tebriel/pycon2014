# Memory Leak Finding #

[tracemalloc](http://pytracemalloc.readthedocs.org)

## view references ##

```python
>>> import gc
>>> data = {'abc': 123}
>>> gc.get_referencts(data)
['abc', 123]
```

You can also use the objgraph project to view references, creates a visual
representation of the references

[objgraph project](http://mg.pov.lt/objgraph/)

Sometimes makes a very large graph if there are many dependencies, so maybe not
first tool, or just for a good overview

## RSS Memory ##

*  Representative for the system
*  Coarse measurement
*  Heap fragmentation
*  Difficult to exploit

## Heap Fragmentation ##

Used 2 MB / RSS 2 MB
[xx]
Allocate 8 MB -> Used 10 MB / RSS 10 MB
[xxxxxxxxxxxxxxxxxx]
Release 8.5 MB -> Used 1.5 MB / RSS 10 MB
- is released but not available to the system again
[xx----x----------x]

## memory_profiler ##

[memory_profiler](http://pypi.python.org/pypi/memory_profiler)

Can be used in some cases, but it can get very complicated and hard to use

## Manual Computation ##

```python
>>> data = {None: b'x' * 10000}
>>> sys.getsizeof(data)
296
>>> sum(sys.getsizeof(ref)
..    for ref in gc.get_referents(data))
10049
```

## Heapy, Pympler, Melia ##

*  List all Python objects:
   `gc.get_objects()`
*  compute the objects size
*  group objects by type (to see which are using the most memory)

### Problems ###

*  Doesn't trace all the memory (ex: zlib)
*  Doesn't provide the origin of objects (where they came from)
*  Difficult to use

__These are all especially difficult on Embedded devies__

## PEP 445: API malloc() ##

*  PyMem_GetAllocator()
*  PyMem_SetAllocator()
*  Replace memory allocators
*  Set up a hook on allocators, something you can call before the allocator
   occurs
*  Implemented in Python 3.4

Tries to decrease heap fragmentation


## PEP 454: tracemalloc ##

Implemented in C

Allocate Memoryo
```python
traces = {}
def trace_malloc(size_):
    ptr = malloc(size)
    if ptr:
        tb = traceback.extract_stack()
        traces[ptr] = (size, tb)
    return ptr
```

To deallocate, just delete the key from traces

### Features ###

*  No overhead when disabled
*  Get the traceback where an object was allocated!!
*  Compute stats per filename, line number or traceback
*  Compute diff between to snapshots (good for diff code paths)

Doesn't cause a memory overhead where not tracing unlike other profilers

Doesn't replace existing tools, but gives more features to existing tools,
meant as an add-in/on

Good to know what module uses the most memory and what line number where the
alloc comes from (and a traceback)

Because it's a simple dictionary, you can easily serialize this dict and then
save it for later

### UI For Comparison of Snapshots ###

[tracemallocqt](https://bitbucket.org/haypo/tracemallocqt)

## tracemalloc backport ##

*  Available at PyPi
*  Require to patch and recompile Python (yikes!)
*  ... maybe also recompile python extensions written in C
*  Patches for Python 2.7 and 3.3
*  Ubuntu packages available

## Display top 10 lines ##

```python
import tracemalloc
tracemalloc.start()
snapshot = tracemalloc.take_snapshot()
top_stats = snapshot.statistics('lineno')
```

## Get object traceback ##

```python
import tracemalloc
tracemalloc.start(25)
tb = tracemalloc.get_boject_traceback(obj)
for line in tb.format():
    print(line)
```

## PEP 445 (API malloc) ##

*  Ticket opened in 2008
*  Patch promised in march 2013
*  Patch committed in june 2013
*  Commit reverted => PEP 445
*  Better API thanks to the PEP
*  BDFL delegate: Antoine


## PEP 454 (tracemalloc) ##

*  Store the traceback, not just 1 frame
*  Code rewritten from scratch
*  Much better API
