# Django, the Good Parts #

*  About 9 years old
*  161,923 Lines of Python in Django 1.7b1
*  Considered a Full Stack Framework
*  Now the literal 800lb. gorilla

## What makes django worth using ##

*  HTTP abstraction + request/response cycle
*  Conservative approach to features
*  Secret weapon (app)

## HTTP Sucks ##

*  9 Diff requewst methods, some safe, some idempotent, some neither, vastly
   different request/response chars
*  Unicode unaware
*  Persistence, auth, streaming, security all tacked on afterthoughts

## How to CGI ##

### How it's supposed to work ###

*  Script invoked by the web server
*  Receive Submitted data over std input
*  Script does processing
*  Send response over stdout

### How it works ###

*  Script invoked by web server, if config'd correctly
*  chmod 777 ALL the things!
*  Environment full of lies and sadness
*  Give up figuring out what the actual requested URL was and fork()-bomb the
   server

## WSGI Pain Points ##

1.  CGI-style environ: have to pass it around, parse, reparse, rereparse, etc
1.  Signaling up and down the stack requires inventing ad-hoc protocols
1.  Return/response API sucks. For Reals.
1.  Inherits HTTP's awful approach to character encoding

## Let's do Better! ##

*  HTTPRequest already ready already for you
*  Sensible attribute and dictionary-based access
*  Relatively sane handling of character encoding
*  HTTPResponse
*  Easy to construct and manipulate
*  Covenience 404/301/etc
*  URL parsing done via regexes

## Life Cycle ##

*  Middleware system baked in (but it sucks, like all do)
*  Signals!
*  Decorators!
*  Call other stuff -- its callables all the way down

## We read PEP 333 so you don't have to ##

*  Django project is a wSGI app
*  wsgipy + WSGI_APPlication

__Sane HTTP/WSGI is worth importing some stuff__

## Conservative Framework, but not minimal ##

*  The truncatechars filter (new in 1.4), takes a string and truncates at a number
   of characters (took 4 years)
*  Migrations took 6 years, things get into django very slowly

## Removals ##

*  contrib[comments|databrowse|localflavor|markup] and probably more
*  Things are difficult to add, easier to remove

## Why isn't this a bad thing, like usual? ##

*  Strong preference for community solutions, wait for a community winner
   instead of adopting the new hotness
*  Core framework more about providing API support instead of features
*  More "swappable" components than expected
*  More stability over time
*  Features land when they're ready
*  Competition (within community) often produces better solutions

## Encapsulation of Applications ##

Django's secret Weapon

*  Django provides a lot of safe apis and assumptions that make integrating
   separate parts easier

