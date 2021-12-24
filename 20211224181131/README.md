# Learning Lab: Liberation Circuit

This is my first learning lab that I made, and this is the solution/write
up for the lab.

The first of the tasks to complete is to compile Liberation Circuit.
After running `./init build && ./init container` to get into the docker
container, all I needed to do was run `make`. Easy enough.

The next task is to configure Liberation Circuit. If this step is skipped
and I just try to run the compiled binary, the error I get when trying to
play the first level is the following.

```
Player 0 spawn failure
Template 0 could not be locked.
Check the template and make sure it's loaded properly.
```

This can be resolved by either running the compiled binary again, or
before running the binary running the following two commands

`mkdir -p ~/.config/linleyh/libcirc`

`cp bin/init.txt ~/.config/linleyh/libcirc/init.txt`

With that, Liberation Circuit is now running!

The last task is to complete the first level, which I just made a bunch
of `attacker` units and rushed the opponent.

There are two extra tasks that are optional, but why not.

The updated `Dockerfile` to compile and run the game as part of the build
looks like the following.

```Dockerfile
FROM alpine:latest
RUN apk update && apk add allegro-dev \
	build-base \
	cmake \
	git \
	make \
	mesa-dri-intel \
	sdl2-dev
RUN git clone https://github.com/linleyh/liberation-circuit.git
WORKDIR liberation-circuit
RUN make -j$(nproc)
RUN mkdir -p ~/.config/linleyh/libcirc
RUN cp ./bin/init.txt ~/.config/linleyh/libcirc/init.txt
WORKDIR bin
CMD ["./libcirc"]
```

The `init container` command does a couple of things. First it checks to
see if the docker container (`$NAME`) is running, and if it is, then
stop/remove it.

Second, it executes `xhost local:root`. Doing `man xhost` shows that
`xhost` is the server access control program for X. Doing `xhost
local:root` is giving the local family access to the X server. It is
important to note that the documentation states the "local family
specifies all the local connections at one. Hoever, the server
interpreted address 'si:localuser:username' can be used to specify a
single local user. (See the Xsecurity(7) manual page for more details.)".

The third thing that is happening is a `docker run`
command passing a few arguments.

`-v /tmp/.X11-unix:/tmp/.X11-unix` is a volume, but what is
`/tmp.X11-unix`? When I do `file /tmp/.X11-unix`, it outputs
`/tmp/.X11-unix/: sticky, directory`. Doing `file /tmp/.X11-unix/*`
results in the following.

```BASH
/tmp/.X11-unix/X0:    socket
/tmp/.X11-unix/X1:    socket
/tmp/.X11-unix/X1024: socket
/tmp/.X11-unix/X1025: socket
```

After some searching, it looks like its a `unix domain socket` for the
`X11` server. X11 is the common window system used on Linux systems. I
will have to ask someone with more Docker experience, why you pass a unix
domain socket as a volume (TODO).

`-e "DISPLAY=unix${DISPLAY}"` is setting an environment variable for the
container called `DISPLAY`. After some searching, I found out that
`$DISPLAY` is an environment variable used by the X window system. In
`man x`, under `DISPLAY NAMES`, it states that the "information is used
by the application to determine how it should connect to the server and
which screen it should use by default (on displays with multiple
monitors)." The display name format is
`hostname:displaynumber.screennumber`. It also states that on "POSIX
systems, the default display name is stored in your DISPLAY environment
variable." Bingo. When I do `echo $DISPLAY`, it outputs `:0`. This means
that the argument is going to result in `DISPLAY=unix:0`, which is
setting the display name for the X window system.

`--device /dev/dri` is adding a host device, but what is `/dev/dri`? From
searching, I have not really found a direct answer, but what it looks
like is `direct rendering infrastructure (DRI)`. DRI is a framework that
the X window system uses to access graphics hardware. This will have to
be another thing I confirm with someone who has more knowledge of Linux/X
(TODO).

`--name $NAME` and `$IMAGE` are self-explanatory.

The fourth, and last thing happening is removing local permissions via
`xhost`.

Related:

* Liberation Circuit
	<https://github.com/linleyh/liberation-circuit>
* Learning Lab: Liberation Circuit
	<https://github.com/oglinuk/lab-liberation-circuit>
* `man unix`
* `man x`
* X Window System
	<https://x.org/wiki/>
* Direct Rendering Infrastucture
	<https://dri.freedesktop.org/wiki/>

Tags:

	#c #ocms #solution #docker #x #gaming
