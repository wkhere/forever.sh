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
