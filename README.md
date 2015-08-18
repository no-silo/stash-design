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

A `stash` notebook is a nested directory structure. Each directory represents a single *document*; a document is comprised of multiple files, that is, all of the regular files contained inside the document directory. Nested directories create child documents.

Filenames with a leading underscore are reserved for implementing meta functionality and must not be assigned to any user data.

With the exception of binary "attachments", everything in Stash is plain-text. Notesbooks can be edited with standard editing tools. Versioning with SCM and syncing via tools like Dropbox is supported.

### Meta Files

Files/folders with a leading underscore have special meaning within a Stash notebook. At present these are:

  * `_tags` (file): unique, only exists at the notebook root. The `_tags` file can be used to organise tags into a hierarchy (one tag per line, indentation implies descendancy). Any tags omitted from this file are assumed to be top-level tags.
  * `_template` (directory): a template document; any new document created at this level will be a copy of this template.

## 2. Client Library

## 3. Command Line Tool

## 4. Web-based Notebook Browser

## 5. Web-based Notebook Editor

## 6. Synchronisation Tools
