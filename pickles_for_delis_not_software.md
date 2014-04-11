## Pickles are for Delis, Not Software ##

`import pickle`

### What is pickle? ###

Serialization Library, turns an object into bytes and then ressurect your
object later

Used for:

*  sending things between processes
*  Storing python objects in database (like memcached)

### What does it do? ###

Dumps into a very non-user readable set of bytes

### How? ###

*  Writes out type specifier
*  write out string representation of the item
*  writes new line

### What happens to your own created classes? ###

Takes apart args and function, then serialzies each of them individually to be
restored later like in previous How? section

### Can I have custom pickle logic? ###

Yes, overwrite __reduce__, return a tuple within a tuple

### Unpickling ###

Pickle is a bit of instructions instead of just a set of data (like JSON)
This is just like RPN calculator


### Security Implications ###

Can serialize untrustable data, system calls, arbitrary python code execution

[Article on Exploiting Pickle](https://blog.nelhage.com/2011/03/exploiting-pickle)

### Migration Implications ###

If a class that was used during pickling, you can't unpickle it.

Changing implementation of an object's details will break unpickling, (not
maintainable, it ties you to the original implementation)

### Alternatives ###

Write a dump method that serializes the important data and a version #
Write a load method, check the version, create an instance of the class with
  the data attrs

__Advantages__

*  More testable
*  Simpler, readable, known data storage format
*  More auditable

Pickle: Unsafe at any Speed, security risks, data migration risks, etc
