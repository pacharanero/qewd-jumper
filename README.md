# qewd-jumper
documentation-driven development repo for an as-yet fictional command line tool

# Purpose
qewd-jumper is a tool for automating the workflow of developing electronic health records using the [Ripple Showcase Stack](http://ripple.foundation/)

Modern web application development was revolutionised by the way that [Ruby on Rails](http://rubyonrails.org/) used convention-over-configuration to remove most of the painful hand-wiring inside a web-application. Simple, predictable namespacing rules were applied to allow Rails to simultaneously generate a database schema with matching Ruby objects, a full suite of methods for getting and setting the attributes of those objects, and user interface scaffolding already configured to work with your Ruby objects.

A really nice way to see this in action is in the original 2005 Rails demo by its creator, David Heinemeier Hansson, on YouTube [here](https://www.youtube.com/watch?v=Gzj723LkRJY)

Prior to this, web application developers had been doing a lot of the internal 'wiring' of software objects to database columns and UI elements by hand. Rails massively augmented developer productivity and paved the way for a panoply of similar frameworks in other languages, such as Django in Python.

Note that this is not an attempt to turn Ripple-Qewd into Ruby on Rails, it's simply a tool for automating away some of the painful handwiring that goes into building an application on openEHR.

-----

# Installation
`npm install qewd-jumper` installs qewd-jumper and all dependencies. The command `jumper` will be added to your $PATH

-----

# Usage
The command `jumper` automates some of the manual processes of using openEHR archetypes.


## `install`
`jumper install template <template-url> [ <template-name> ]`

### actions
* pulls the relevant openEHR template from the CKM where it is stored
* installs the operational template into your EtherCIS instance and restarts EtherCIS

### parameters
`<template-url>` is the URL at which to find the ADL file of the template you want to install
`<template-name>` is a user-defined internally-used name for the template, which you can then use with the other qewd-jumper commands to refer to the template you're installing. If omitted, this parameter defaults to the text within the template's <name> tags in the XML 

### example


## `generate`
`jumper generate qewd <template-name>`

### actions
In QEWD (Middleware):
* auto-generates the correct AQL for GET querying the template
* auto-generates the correct JSON for POST creating/updating the template
* exposes a REST interface for your frontend application, using a predictable regular namespacing methodology

### parameters

### example


`jumper generate pulsetile <template-name>`

### actions
In Pulsetile (User Interface):
* generates a scaffold webform conforming to the data types of each field
* generates 

### parameters

### example


## `pull`
`jumper pull template <template-url> ( <template-name> )`
pulls the template from the given URL without installing it into EtherCIS, for when developing on 


## `uninstall`
`jumper uninstall <template-name>`

### parameters

### example

-----

# License
This work is open source software, free to us without warranty, under the Apache 2 license. See LICENSE.md for further details
