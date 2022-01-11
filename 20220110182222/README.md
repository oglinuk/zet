# TLCL: 2 - Navigation

The commands introduced in this chapter are `pwd`, `ls`, and `cd`.

Before continuing, it is important to note that all command output will
be using a docker container, running the `bash:5.1` docker image. This
means that the shell is run as root and will miss a lot of what a typical
Linux distribution will have.

Before we get into the commands, we need to understand the *file system*
or structure of Linux. In a paper written by Dennis Ritchie titled "The
Evolution of the Unix Time-sharing System", he describes "Besides the
financial agitations that took place in 1969, there was technical work
also. Thompson, R. H. Canaday, and Ritchie developed, on blackboards and
scribbled notes, the basic design of a file system that was later to
become the hear of Unix." A little bit into the paper he describes
"Structurally, the file system of PDP-7 Unix was nearly identical to
today's. It had ..."

```
1) An i-list: a linear array of *i-nodes* each describing a file. An
i-node contained less than it does now, but the essential information was
the same: the protection mode of the file, its type and size, and the
list of physical blocks holding the contents.

2) Directories: a special kind of file containing a sequence of names and
the associated i-number.

3) Special files describing devices. The device specification was not
contained explicitly in the i-node, but was instead encoded in the
number: specific i-numbers corresponded to specific files.
```

One key difference between Unix-like systems and Windows is how drives
are mounted. Unix-like systems, regardless of how many drives, are
mounted under one file system. Windows creates a separate file system for
every drive.

The `pwd` command outputs `/`. This is called the *current working
directory*.

The `ls` command outputs

```
bin
dev
etc
home
lib
media
mnt
opt
proc
root
run
sbin
srv
sys
tmp
usr
var
```

The `cd` command doesn't output anything, but we can use it to change
into one of the directories shown from the `ls` command. Let's `cd` into
`dev` and `ls`. 

```
core
fd
full
mqueue
null
ptmx
pts
random
shm
stderr
stdin
stdout
tty
urandom
zero
```

Learning to navigate Linux also introduces the concept of *absolute* and
*relative* paths.

An absolute path starts with the root (`/`) directory and continues down
the file system tree until the desired directory or path is found. An
example of an absolute path would be `/dev/pts` or `/bin`.

A relative path starts from the current working directory and uses
special notations (`.` and `..`). The `.` refers to the current working
directory, and `..` refers to the parent directory. An example of a
relative path would be `./usr/bin`.

A few important things to remember.

* filenames and commands are case sensitive (`ls` is different to `Ls` and `lS`)
* Unix has no "file extension", and so you can name files anything
* Even though there is support for long filenames, *do not use spaces*

Related:

* TLCL
	<https://www.linuxcommand.org/tlcl.php/>
* FHS
	<https://wiki.linuxfoundation.org/lsb/fhs>
* The Evolution of the Unix Time-sharing System
	<https://www.bell-labs.com/usr/dmr/www/hist.pdf>

Tags:

	#tlcl #shell #unix #filesystem
