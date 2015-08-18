# stash

`stash` is an open-source data format and associated toolchain for managing structured notebooks, featuring an extensible mixed-mode content model, dynamic documents and inter-document linking. Think of it as Evernote for power users.

As it stands this document is a brain dump of what 

Very little code is currently written, mostly existing as a collection of ad-hoc bash, Ruby and Javascript scattered about my local machine.

## High Level Overview

The `stash` ecosystem comprises:

  1. a specification for the filesystem layout of a notebook
  2. a client library providing programmatic access to (1)
  3. a command line tool that builds on (2) to provide a REPL-like access to (1). Supports both querying and modfication.
  4. a web-based notebook browser
  5. a web-based notebook editor
  6. synchronisation/publication tools

This is the long-term vision. Lots to do, but possible to build incrementally.

## 1. Notebook Filesystem Layout

A `stash` notebook is a nested directory structure. Each directory represents a single *document*; a document is comprised of multiple *files*, that is, all of the regular files contained inside the document directory. Nested directories create child documents.

Filenames with a leading underscore are reserved for implementing system functionality and must not be assigned to any user data.

With the exception of binary "attachments", everything in `stash` is plain-text. Notesbooks can be edited with standard editing tools. Versioning with SCM and syncing via tools like Dropbox is supported.

### File Types

`stash` places particular importance on file types; within a document, a file's type is derived from its extension. The primary file types are:

#### `md`

Markdown text.

#### `info`

Structured data. The data format will be based on YAML, but with variations. In particular:

  * date/time types
  * embedded s-expressions
  * document reference syntax

Example `info` syntax:

```
title: My new document
date: 2015-08-19 00:23
query: (and (tag foo) (tag bar))
tags: [a, b, c]
next: #document2
```

#### `pdf`,`jpg`,`png` etc.

Arbitrary files can be added as attachments.

#### `query`

Executes a dynamic query against the notebook using an s-expression syntax and embed live results on the page.

Example query, finds all documents tagged with "programming" or whose title includes the same string.

```
search: (or (tag programming) (title (i-match "programming")))
```

#### `multi`

Multi-docs allow various types of content to be included in a single document. Content can be either inline, or embedded from another file within the same document.

Multi-doc example:

```
--- markdown

# This the document title

Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse
cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non
proident, sunt in culpa qui officia deserunt mollit anim id est laborum.

--- query

search: (tag foobar)

--- embed: summary.pdf
--- embed: notes.md

### `meta.info`

A document's optional `meta.info` file contains strucuted metadata describing the document. Data inside `meta.info` forms the basis of the structured data that can be queried by the `stash` client library.

Arbitrary metadata is supported, however the following top-level keys have particular significance:

  * `title`: document title
  * `tags`: array of tags

### System Files

Files/folders with a leading underscore have special meaning within a `stash` notebook. At present these are:

  * `_tags` (file): unique, only exists at the notebook root. The `_tags` file can be used to organise tags into a hierarchy (one tag per line, indentation implies descendancy). Any tags omitted from this file are assumed to be top-level tags.
  * `_template` (directory): a template document; any new document created at this level will be a copy of this template.

## 2. Client Library

## 3. Command Line Tool

## 4. Web-based Notebook Browser

## 5. Web-based Notebook Editor

## 6. Synchronisation Tools
