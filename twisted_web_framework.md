# Twisted #

out of box can run:

*  DNS
*  Chat
*  Http
*  FTP
*  more

[Twisted Bittorrent Client](https://github.com/staceysern/bittorrent)

## What is Twisted? ##

Event-driven network engine, provides lots of building box for networked
applications, lots of help for standard protocols. Also provides tools for
implementing your own protocols.

Is event-driven like Node.js.

__Single-threaded synchronus__ applications cause lots of blocking time spent
waiting

__Multi-threaded synchronous__ applications can handle multiple tasks
simultaneously, but still block once max # of threads is reached, and still
lots of time spent waiting.

__Event driven__ applications uses event loop to run tasks each one-at-a-time
but will yield execution instead of blocking while waiting

## Event Loop (Reactor) ##

*  Start up and listen to TCP/UDP/SSL
*  Maintains a uniform programming interface across all platforms for ease of
   coding
*  _Deferred_ provides a __callback chain__ and an __errback chain__
