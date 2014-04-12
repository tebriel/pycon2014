# Designing Django's Migrations #

NOT: Moving South into Django, instead "Adding migrations to Django"

## SchemaEditor ##

*  Abstracts schema ops across DBs
*  Works in terms of django fields/models
*  Contains per-database workarounds

South has the issue of being table related insted of model related, so falls
short on more advanced datatypes

## django.db.migrations ##

*  Migration file reader/writer
*  Dependency Resolver
*  Autodetector
*  Applied/unapplied tracking

## New Migration Format ##

Old one is very large, verbose, and hard to read

### Desires ###

*  More consise

Now a series of operations on a model

## In Memory running ##

*  Creates models from migration sets
*  Autodetector diffs created from on-disk

## Database Pecurliarities ##

*  PostgreSQL
  *  Great, no issues
*  MySQL
  *  No transaction DDL
  *  No CHECK constraints
  *  Conflates UNIQUE and INDEX
  *  When migration fails, no way to roll back
*  Oracle
  *  Different SQL syntax
  *  Picky about names
  *  Can't convert to/from TextField (LOB)
*  SQLite
  *  AAAAAAAAAHHHHHHHHHH
  *  Altering tables? Schema introspection? What?
  *  No delete column, alter column, no way to see schema
  *  Very hard to work with
  *  Good for embedded, not for production, migrations, etc

## Backwards Compatability ##

*  Django generally very good at this
*  Auto-applies first migration if tables exist
*  Ignores South-style migrations

## Lessons Learnt ##

*  Explicit is better than implicit
*  A lot of things in south is very implicit, gets confusing and hard to resolve
*  Abstracting DBs is Hard
*  Composability Rocks
*  Feedback is Vital
  *  people use it in very strange, dirty ways, they gave me good feedback and
     bug reports

Scheduled Released Mid-May/Late-May
