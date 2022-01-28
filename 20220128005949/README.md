# How to play Quake (1996)

Quake along side DOOM, is one of the most iconic games there are (in my
opinion). In my last zet I documented how to play DOOM (1993), and in
this zet I am going to document how to play Quake (1996).

Unlike DOOM, there is not currently a finished free version of the game
data, so you will need to purchase the game from GOG or steam and copy
the game files (`id1` directory).

I would like to note that there is a project (in development) similar to
Freedoom, called LibreQuake. The project aims to create a free, community
built version of Quake. You can find a reference link below.

Like DOOM, there are numerous source ports available. It is important to
note that unlike DOOM source ports, which commonly support DOOM 1 and 2,
not many source ports support more than one Quake game. I suggest using
the `DarkPlaces` source port.

Download the source code at <https://gitlab.com/xonotic/darkplaces>.

Move the game files (`id1` directory) you copied from GOG or steam into
the `darkplaces` directory and change into the directory.

If you have access to a terminal, then compile the C code by running
`make`.

`./darkplaces-sdl` to run the game.

Enjoy!

> Bethesda acquired Id Software, and have made a remake called "Quake:
> The Offering". I do not know if this game is different, but it looks
> like you can't purchase the non-remake version. Need to confirm this.

Related:

* Original Quake source code
	<https://github.com/id-software/quake>
* DarkPlaces source port
	<https://icculus.org/twilight/darkplaces/readme.html>
* LibreQuake
	<https://github.com/misslav/librequake>

Tags:

	#quake #darkplaces #c #make #librequake
