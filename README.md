watchDirectory
==============

Similar to node fs.watchFile but watches a directory recursively and lets you unwatch as well

## Purpose

This module provides the ability to recursively watch a directory for changes.
Unlike all the other similar modules, this one can unwatch directories as well, which is why I wrote it.

#### require('watchdir').watchDirectory(root, [options,] callback)

The first argument is the directory root you want to watch. 

The options object is passed to fs.watchFile but can also be used to provide additional watchDirectory specific options:

* `'initial'` - Defaults to true.  If true then we notify the callback of files during initial directory walk.
* `'recursive'` - Defaults to true.  Controls the depth of our directory walk.
* `'filter'` - Can be a function or RegExp or string.  If it's a string then that will be considered an extension to check.  Your callback will only be notified about files that pass your filter.

<pre>
  watchdir.watchDirectory('src', {filter:'.js'}, function (filename, curr, prev, change) {
    if (change == 'created') {
      // filename is a new file
    } else if (change == 'deleted') {
      // filename was removed
    } else { // change == 'modified'
      // filename was changed
    }
  })
</pre>  