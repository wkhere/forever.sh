## forever

A simplified "run my stuff when source code changes" tool.
For Linux and OSX.

### Intro

Over years I wrote several mutations of a script which monitors source code changes
and triggers some action when they changed. The last invention was [forever.py],
aimed esp. towards writing RubyMotion code for iPhone on OSX.
[forever.py]: http://github.com/herenowcoder/forever.py

That was smart, but not working on Linux, where instead I used bunch of inotify-based
scripts. Also, the adoption to different file layouts ended up as modifying the scripts
which were supposed to be generic. That was simply wrong.

Now this is how I believe it should be. `forever` hides the difference between Linux/OSX
file monitoring and just runs your per-project `./forever.step` script on each change.
You define the list of files by printing it out when running `./forever.step files`.
That's it.

### Installation
```shell
% wget https://github.com/herenowcoder/forever/raw/master/forever -Oforever
% chmod a+x forever
% ... put it in your PATH
```

### Usage
* cd to your project dir
* prepare `forever.step` file like this one:
```shell
#!/bin/bash -e

if [ "$1" == files ]; then
    find . -type f -name '*' #... here discover files to watch
    exit
fi

echo "FOO!" #... here you usually compile and/or run your tests
```
* remember to `chmod a+x forever.step`
* run it forever ;)
```shell
% forever
[forever started 14:27:25]
FOO!
0.00 user 0.00 system 85.13% cpu 0.003 total
```
Now when you save files, it goes like:
```
[forever awakened 14:45:53]
FOO!
0.00 user 0.00 system 95.09% cpu 0.004 total
```
..until you hit Ctrl-c.

You usually want to have the same or very similar `forever.step`
for the same kind of language/application. Here's [example stepfile]
(https://github.com/herenowcoder/forever/blob/master/examples/forever.step-elixir)
for an [Elixir] project,
running compilation & tests, plus regenerating [ctags] in background.

[Elixir]: http://elixir-lang.org
[ctags]: http://ctags.sourceforge.net
