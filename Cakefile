wd = require './main'
cs = require 'coffee-script'
cp = require 'child_process'

exec = (command, callback) ->
    cp.exec command, (err, stdout, stderr) ->
        console.log err if err?
        console.log stdout.toString() if stdout?
        console.log stderr.toString() if stderr?
        callback?()

task 'watch', 'watches this directory for changes', ->
    wd.watchDirectory '.', {filter:'.coffee'}, (filename, change) ->
        console.log filename, change

task 'build', 'builds this project', ->
    exec 'coffee -c .'


