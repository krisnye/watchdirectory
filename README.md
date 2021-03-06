watchdirectory
==============

Similar to node fs.watchFile but watches a directory recursively and lets you unwatch as well

## Install

<pre>
  npm install watchdirectory
</pre>

## Purpose

This module provides the ability to recursively watch a directory for changes.
Unlike similar modules, this one can unwatch as well.

#### watchdirectory.watchDirectory(root, [options,] callback)

The first argument is the directory root you want to watch. 

The options object is passed to fs.watchFile but can also be used to provide additional watchDirectory specific options:

* `'initial'` - Defaults to true.  If true then we notify the callback of files during initial directory walk.
* `'recursive'` - Defaults to true.  Controls the depth of our directory walk.
* `'include'` - Can be a function or RegExp or string.  If it's a string then that will be considered an extension to check.  Your callback will only be notified about files that match.
* `'exclude'` - Can be a function or RegExp or string.  If it's a string then that will be considered an extension to check.  Your callback will not be notified about files that match.

<pre>
  var unwatch = watchdirectory.watchDirectory('src', {filter:'.js'}, function (filename, curr, prev, change) {
    if (change == 'initial') {
      // filename found during initial pass
    }
    else if (change == 'created') {
      // filename is a new file
    }
    else if (change == 'deleted') {
      // filename was removed
    }
    else if (change == 'modified') {
      // filename was changed
    }
  });

  // later on to unwatch, just call the previously returned function
  unwatch();
</pre>  