## forever.sh

**NOTE** this is superseded by https://github.com/wkhere/forever

A simplified "run my stuff when source code changes" tool.
For Linux and OSX.

`forever.sh` hides the difference between Linux/OSX file monitoring 
and just runs your per-project `./.forever.step` script on each change.
You define the list of files by printing it out when running `./.forever.step files`.

### Installation
```shell
% curl -OL https://github.com/wkhere/forever.sh/raw/master/forever.sh
% chmod a+x forever.sh
% ... put it in your PATH
```

### Usage

#### Elixir

`forever.sh` discovers a `mix` project and prepares `.forever.step` script
if it is not present.

#### General

* cd to your project dir
* prepare `.forever.step` file like this one:
```shell
#!/bin/bash -e

if [ "$1" == files ]; then
    find . -type f -name '*' #... here discover files to watch
    exit
fi

echo "Hey!" #... here you usually compile and/or run your tests
```
* remember to `chmod a+x .forever.step`
* run it forever ;)
```shell
% forever.sh
[forever.sh started 14:27:25]
Hey!
0.00 user 0.00 system 85.13% cpu 0.003 total
```
Now when you save files, it goes like:
```
[forever.sh awakened 14:45:53]
Hey!
0.00 user 0.00 system 95.09% cpu 0.004 total
```
..until you hit Ctrl-c.
