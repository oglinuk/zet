# How to play DOOM (1993)

DOOM is easily (in my opinion), one of the most iconic games ever made.
It is enjoyable to play even to this day. The best part of DOOM is the
fact that it has been made open source under a permissive license. From
this there have been many source ports of the original DOOM code. Id
software was ahead of their time, in more ways that one. One of the
amazements are the WAD files.

In this zet I am going to show you how to to play an entirely free
version of DOOM called Freedoom.

To play a game you need two things: a game engine and game data. The key
thing to remember with things like DOOM and Quake is that the game
*engines* are free *not the data*. Fortunately, because of the genius of
Id software game files, all you need to do is purchase the games from a
platform like GOG or steam. You can then navigate to where the game is
installed locally and copy the game files. DOOM game files are called
"Wheres All the Data" or "WAD" files.

Freedoom is an open source project to create a free, community developed
version of DOOM. This means that we now have not only free game engines,
but free game data!

To play DOOM you will first need a source port. I highly recommend
`chocolate-doom`, since it's goal is to be as historically accurate to
the original engine as possible.

You will need to download the source code available at
<https://github.com/chocolate-doom/chocolate-doom>.

To find out how to build chocolate doom for your specific platform,
please refer to `Building Chocolate Doom on ...` below.

Then download `Freedoom: Phase 1+2` available at
<https://freedoom.github.io/download.html>.

If you have access to a terminal, you can compile the source code via
the following.

```
autoreconf -fiv
./configure
make
```

`./chocolate-doom -iwad <PATH TO freedoom1.wad>` to run the game.

*That's it*. ***dOOOOOOOM on!***

Related:

* Original DOOM source code
	<https://github.com/id-software/DOOM>
* Freedoom
	<https://freedoom.github.io/>
* DOOM WAD file
	<https://doom.fandom.com/wiki/WAD>
* Building Chocolate Doom on ...
	<https://www.chocolate-doom.org/wiki/index.php?search=Build&title=Special%3ASearch&go=Go>
* Download `Freedoom: Phase 1+2`
	<https://github.com/freedoom/freedoom/releases/download/v0.12.1/freedoom-0.12.1.zip>
* Freedoom
	<https://freedoom.github.io>
* DOOM Source Ports
	<https://doomwiki.org/wiki/Source_port>

Tags:

	#doom #freedoom #chocolate-doom #c #autoconf #make
