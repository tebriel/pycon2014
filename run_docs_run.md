# Executeable documentation #

[Slides](http://tinyurl.com/rundocsrun)

## Problems ##

*  Forget key details in how it works
*  Examples should change as implementation does
*  It's kind of boring to do

## Solution ##

Code your doc!

### Self Verifying ###

*  Will alert you if it fails
*  Fun to write
*  Good exercise

## Doctests ##

*  Docstrings can/should include usage samples
*  Lets you know when docstrings fail
*  Orthogonal to your unit testing
*  New name: "Executable Docstrings"

## Sphinx ##

*  Takes reST and creates documentation
*  Use with doctest type strings
*  Also has an autodoc extension which can run through your code, can find
   doctests this way and will execute them
*  autorun (not included by default), lets you write code for examples and just
   outputs the result into the docs
*  sphinxcontrib.programoutput is similar to autorun (gives you the shell)

### Advantages to Sphinx ###

*  Great structure
*  Lots of hosting options
*  Many file type formats (PDF, ePub, LaTeX)

## Shout-outs ##

[literate-resting](https://github.com/ged-lab/literate-resting) - shell script
to preprocess console commands in reST

[sphinxcontrib-autoprogram](https://pythonhosted.org/sphinxcontrib-autoprogram/)
- reads argparse, autogenerates doc for sphinx

## IPython Notebook ##

*  Beautiful example of executable documentation

### Serving These ###

*  Your own server
*  nbviewer + URL or gist (static)
*  [wakari.io](http://wakari.io) will host live notebooks

### Advantages ###

*  User can experiment/mess with the details
*  Great hosting options

## dexy ##

*  Framework for applying transformations to documents
*  Allows more freedom in presentation of data, but harder to configure, more
   steps
*  Uses jinga templates

### Advantages ###

*  Lots of built-in transofmrations
*  Tons of Transformations (called filters)
*  Very precise control over output

### Warnings ###

*  Harder to use (need manual `dexy reset` needed)
*  Incomplete Docs (LOL)


## Possibilities ##

*  Living Lecture Notes
*  Tutorials that can assist with config
*  Live troubleshooting docs
*  Information-rich Dashboards
*  Compliance documents that are self-verifying
