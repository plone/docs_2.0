# Documentation 2.0

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Documentation 2.0](#documentation-20)
	- [Introduction](#introduction)
	- [Improvements](#improvements)
		- [Appearance](#appearance)
		- [Audience](#audience)
		- [Style](#style)
		- [Structure](#structure)
			- [README Removal](#readme-removal)
			- [External Removal](#external-removal)
			- [Splitting](#splitting)
		- [Search](#search)
		- [Branches](#branches)
	- [Testing](#testing)
		- [CI](#ci)
		- [Tests On Commits](#tests-on-commits)
		- [Tests On All Docs](#tests-on-all-docs)
		- [Redactor](#redactor)
		- [Test Overview](#test-overview)
	- [Building](#building)
		- [Coster](#coster)
	- [Deploying](#deploying)
		- [Coster](#coster)
		- [Hosting](#hosting)
	- [Helper Tools](#helper-tools)
		- [Henry](#henry)
		- [Coster](#coster)
		- [Redactor](#redactor)

<!-- /TOC -->

 ## Abstract

- Goals: User focused, Modern, Lessons Learned

## Introduction

- Some words about current state and what we can do better

## Improvements

### Appearance

Make the _look and feel_ better, make it easier for people to _identify_ and find what they are looking for. This can be done for example with a improved landing-page, with visual improvements and adding _boxes_ per audience.

**Example**

![alt text](https://raw.githubusercontent.com/plone/docs_2.0/master/_static/new_docs_landing.png "Example Docs Landing ")

Use a theme which is focused on presenting content !

If you "click" on the box with your audience you get immediately to the parts of the docs you are looking for, for example "theming" and then you only see the theming docs, if you click "here" on search you get a custom search (with a button) to search all docs, too.

"Rethink" our terms, for "us" (old plone ppl) lots of our terms makes sense but that is not always the case for newer people. We should try to adopt that.

Examples of content focused themes with less visual interruptions

**Redactor Theme**

![alt text](https://raw.githubusercontent.com/plone/docs_2.0/master/_static/redactor_theme.png "Redactor Theme")

**TTD Henry**

![alt text](https://raw.githubusercontent.com/plone/docs_2.0/master/_static/henry_own_docs.png "Henry Theme")

**TTD Docs**

![alt text](https://raw.githubusercontent.com/plone/docs_2.0/master/_static/docs_ttd.png "TTD Docs")

### Audience

Better and easier distinction between audiences. If a user is looking for the docs about theming the user is at this moment not interested in docs about ZEODB.

To do so we need to make sure that all docs in the different categories are really:

- _straight to the point_
- written in the right tone and voice for the category
- understandable
- the user does not get distracted with to much **noise** (like look and feel, etc)

### Style

- shorter items
- consistent style-guide and usage of terms
- consistent and shorter headings

### Structure

#### README Removal

Currently we are including _READMEs_ from _external_ documentation like [bobtemplates.plone](https://github.com/plone/bobtemplates.plone).

A _README_ is great for a developer, unfortunately it is less suited for including into documentation.

Besides the wrong tone and goals of a _README_ also the nice buttons of Travis etc are no addition to the docs.

They only add _noise_ and distraction.

These are perfectly fine for a _README_ but less cool in the documentation.

![alt text](https://raw.githubusercontent.com/plone/docs_2.0/master/_static/readme_screen_red_box.png "README in Docs")

#### External Removal

Because of _historical_ reasons and the way how the current documentation got structured we still use the directory _external_.

This is maybe nice and logical for the _docs team_ but this add no extra value for the reader.

Besides that, it also can lead to confusion, because for the (new) reader it is not clear _why_ certain parts of the docs are located under _external_.

Further is breaks with the structure and consistency of the docs.

![alt text](https://raw.githubusercontent.com/plone/docs_2.0/master/_static/external_removal.png "Removal of external dir")

#### Splitting

(standalone)

Improve the structure by moving some parts to other locations. Our current structure does is not always logical or understandable for (new) developer.

We can improve that by re-locating some parts to other locations and by 'merging' some parts into one chapter. Examples are here: Installation and developer docs.

I am sure there are more places where we can do that.

Further remove/improve the structure to make the docs less **nested**.

It is often confusing for user that some docs are really **deep** nested like _docs.plone.org/develop/bla/bla/bla/bla_

List of other structure improvements:

- remove **/external**
- remove **READMEs** of docs we include

**ToDo** Screen of README in docs

### Search

- custom search per _audience_ like searching only in _theming_ or _installing_
- better **docs.plone.org/search** atm the mix between Agolia and Sphinx is confusing, create a **/search** with Agolia API.

### Branches

There is already a open issue for that, we will change the way how the docs are branched.

## Testing

### CI

We will use a dedicated CI setup for the docs. All tests are running in containers, meaning we can use them better, faster and everywhere.

### Tests On Commits

The way how we run tests will change. With the new setup we will test with each commit or PR only the files which are changed.

This has the following advantages:

- tests are faster
- we can better and 'easier' improve the docs and its tests
- it is less de-motivating for people, since CI is "only" complaining about "their" commits.
- tests are based on Redactor

### Tests On All Docs

### Redactor

This is our new test-framework where we can configure the amount of tests and also the level, etc. Some of the tests we "only" run on release time, like HTML, other ones like style-guide we run **always**.

### Test Overview

- spell-check
- link-check
- line-length
- file-length
- write-good
- style-guide
- white-spaces
- HTML
- ...
- ....

## Building

### Coster

Coster is the re-written and improved version of papyrus. Here we configure which "external" (like ansible-playbooks and branch) docs we fetch and where we put these in our docs.

Coster can handle _rst_ and _md_ !

Coster also fetches all images we need which are created by our jenkins-robots.

After Coster is done fetching and building the docs, we do run again tests on the created HTML, like HTML validation, accessibility checks, etc, etc.

Is these pass, Coster will create automatically "ready to run" container images (docker).

## Deploying

Each version in own container, plus weekly builds of 'unreleased'

Each version like 3, 4, 5 gets a own container.

### Coster

pushes to Docker Hub

See above, Coster creates, tags and uploads the container to Docker Hub.

For "unstable" this will be done, once a week or so.

This is also perfect for local usage, "just" do

```bash
docker pull plone/documentation/5
```

and you get the latest docs of Plone 5.x which you can run locally and also off-line.

Or do

```bash
henry serve
```

### Hosting

k8 recognizes if there is an new image available and automatically downloads and switched (blue-green) to the new image.

## Helper Tools

### Henry

(add henry docs overview)

### Coster

(add coster docs overview)

### Redactor

(note you can run tests also without Redactor)
