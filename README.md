# Firepad

[![Build Status](https://travis-ci.org/firebase/firepad.svg?branch=master)](https://travis-ci.org/firebase/firepad)
[![Version](https://badge.fury.io/gh/firebase%2Ffirepad.svg)](http://badge.fury.io/gh/firebase%2Ffirepad)

[Firepad](http://www.firepad.io/) is an open-source, collaborative code and text editor. It is
designed to be embedded inside larger web applications. 

## Live Demo

Visit [firepad.io](http://demo.firepad.io/) to see a live demo of Firepad in rich text mode, or the
[examples page](http://www.firepad.io/examples/) to see it setup for collaborative code editing.

[![a screenshot of demo.firepad.io including a picture of two cats and a discussion about fonts](screenshot.png)](http://demo.firepad.io/)

## Setup
Firepad uses [Firebase](https://www.firebase.com/?utm_source=firepad) as a backend, so it requires no server-side
code. It can be added to any web app by including a few JavaScript files

```HTML
<!-- Firebase -->
<script src="https://cdn.firebase.com/js/client/2.0.2/firebase.js"></script>

<!-- CodeMirror -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/codemirror/4.3.0/codemirror.js"></script>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/codemirror/4.3.0/codemirror.css"/>

<!-- Firepad -->
<link rel="stylesheet" href="https://cdn.firebase.com/libs/firepad/1.1.0/firepad.css" />
<script src="https://cdn.firebase.com/libs/firepad/1.1.0/firepad.min.js"></script>
```

and calling an init function.

```HTML
<div id="firepad"></div>
<script>
  var firepadRef = new Firebase('<FIREBASE URL>');
  var codeMirror = CodeMirror(document.getElementById('firepad'), { lineWrapping: true });
  var firepad = Firepad.fromCodeMirror(firepadRef, codeMirror,
      { richTextShortcuts: true, richTextToolbar: true, defaultText: 'Hello, World!' });
</script>
```
    
Firepad supports rich text editing with [CodeMirror](http://codemirror.net/) and code editing via 
[ACE](http://ace.c9.io/). Check out the detailed setup instructions at [firepad.io/docs](http://www.firepad.io/docs).

### What's Here

Here are some highlights of the directory structure and notable source files:

* `dist/` - output directory for all files generated by grunt (`firepad.js`, `firepad.min.js`, `firepad.css`, `firepad.eot`).
* `examples/` - examples of embedding Firepad.
* `font/` - icon font used for rich text toolbar.
* `lib/`
    * `firepad.js` - Entry point for Firepad.
    * `text-operation.js`, `client.js` - Heart of the Operation Transformation implementation.  Based on
      [ot.js](https://github.com/Operational-Transformation/ot.js/) but extended to allow arbitrary
      attributes on text (for representing rich-text).
    * `annotation-list.js` - A data model for representing annotations on text (i.e. spans of text with a particular
      set of attributes).
    * `rich-text-codemirror.js` - Uses `AnnotationList` to track annotations on the text and maintain the appropriate
      set of markers on a CodeMirror instance.
    * `firebase-adapter.js` - Handles integration with Firebase (appending operations, triggering retries,
      presence, etc.).
* `test/` - Jasmine tests for Firepad (many of these were borrowed from ot.js).

## Contributing

We love pull requests. If you'd like to contribute to Firepad, run the following commands to get your environment set up:

```bash
$ git clone https://github.com/firebase/firepad.git
$ cd firepad                # go to the geofire directory
$ npm install -g grunt-cli  # globally install grunt task runner
$ npm install -g bower      # globally install Bower package manager
$ npm install               # install local npm build / test dependencies
$ bower install             # install local JavaScript dependencies
$ grunt watch               # watch for source file changes
```

`grunt watch` will watch for changes in the `/lib/` directory and lint, concatenate, and minify the
source files when a change occurs. The output files are written to the `/dist/` directory.

You can run the test suite by navigating to `file:///path/to/firepad/tests/index.html` or via the
command line using `grunt test`.

## Getting Started with Firebase

Firepad requires Firebase in order to store data. You can
[sign up here](https://www.firebase.com/signup/?utm_source=firepad) for a free account.

## Getting Help

Join our [Firepad Google Group](https://groups.google.com/forum/#!forum/firepad-io) to ask
questions, request features, or share your Firepad apps with the community.

