# qewd-jumper
documentation-driven development repo for an as-yet fictional command line tool

# Purpose
**qewd-jumper** is a tool for automating the workflow of developing electronic health records using the [Ripple Showcase Stack](http://ripple.foundation/) to make it more developer-friendly and more like modern web development tooling.

Modern web application development was revolutionised by the way that [Ruby on Rails](http://rubyonrails.org/) used convention-over-configuration to remove most of the painful hand-wiring inside a web-application. Simple, predictable namespacing rules were applied to allow Rails to simultaneously generate a database schema with matching Ruby objects, a full suite of methods for getting and setting the attributes of those objects, and user interface scaffolding already configured to work with your Ruby objects.

A really nice way to see this in action is in the original 2005 Rails demo by its creator, David Heinemeier Hansson, on YouTube [here](https://www.youtube.com/watch?v=Gzj723LkRJY)

Prior to this, web application developers had been doing a lot of the internal 'wiring' of software objects to database columns and UI elements by hand. Rails massively augmented developer productivity and paved the way for a panoply of similar frameworks in other languages, such as Django in Python.

### Manual Ripple/openEHR setup tasks at things are now
Currently when setting up the Ripple Showcase stack, there are a number of manual tasks to be undertaken:

*In the openEHR clinical document repository:*
* select openEHR templates from Clinical Knowledge Manager, requiring (significant domain knowledge to do correctly)
* creation of .oet operational templates from each template
* installation of the template into openEHR CDR (different for each CDR)
* restarting the CDR or otherwise initialising the new templates

*In middleware, integration layer or web application:*
* custom configuration of application/middleware object model and/or REST URL routing to match the interface exposed by the openEHR CDR

*In user interface or front end framework:*
* build UI from scratch using existing components provided by PulseTile UI framework

Use of a decoupled external command utility to automate this setup 'boilerplate' enables the tooling to remain agnostic as to the choice of UI/frontend, middleware/application, and openEHR CDR. This project will initially concentrate on the Ripple showcase stack - [Pulsetile](https://github.com/PulseTile/PulseTile) UI (available in both [Angular](https://angular.io/) or [React](https://reactjs.org/) flavours)  [QEWD](https://github.com/robtweed/qewd) middleware, and [EtherCIS](https://github.com/ethercis/ethercis) openEHR repository. However in the future, the scope of the toll could be extended by the use of plugins to enable it to configure other combinations of openEHR stack.

### Things that qewd-jumper does for you
Qewd-jumper reduces the work involved in setting up the Ripple stack:

* provides curated groups of basic templates to provide functionality for common clinical requirements
* simplifies the steps required to download and install these templates
* automates generation of .oet operation templates
* automates installation of the operational templates in the CDR

*In middleware, integration layer or web application:*
* scaffolds middleware functionality for CRUD operations on the data nodes introduced by the template
* auto-generates correct AQL strings to enable GET/querying of the CDR
* generates any JSON strings required for POST/writing to the CDR
* builds additional helper functions/methods that simplify interaction with the data in the repository, grouping queries which the Pulsetile UI commonly requires (eg. building convenience functions which return all the information for the PulseTile `header-toolbar` element in a single UI query).

*In user interface or front end framework:*
* simplifies the installation of PulseTile UI components, which have *'batteries included'*, meaning they 
* ensures consistent, predictable, human-and-machine-readable namespacing throughout the stack: from UI element/component through the middleware to the backend CDR.

Note that this is not an attempt to turn Ripple-Qewd into Ruby on Rails, it's simply a tool for automating away some of the painful handwiring that goes into building an application on openEHR.

-----

# Installation
`npm install -g qewd-jumper` installs qewd-jumper and all dependencies. The command `jumper` will be added to your $PATH

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
`$ jumper install http://www.openehr.org/ckm/openEHR-EHR-EVALUATION.health_risk.v1
`successfully importe http://www.openehr.org/ckm/openEHR-EHR-EVALUATION.health_risk.v1`
`into openEHR Clinical Document Repository at https://localhost:8089`


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
