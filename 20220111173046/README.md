# TLCL: 3 - Exploring the System

This chapter introduces command *options* and *arguments*, along with the
`file` and `less` commands.

Typically a command will have one or more options, which are generally a
single character with a `-` prefix (`-a`). It is important to remember
that you can combine multiple short options (`-abc`). Commands also
usually support *long options*, which is a word with a `--` prefix
(`--all`).

To see the options a command has, you can add `--help` to the end of the
command and it will output something like the following (`ls --help`)

```
BusyBox v1.33.1 () multi-call binary.

Usage: ls [-1AaCxdLHRFplinshrSXvctu] [-w WIDTH] [FILE]...

List directory contents

	-1	One column output
	-a	Include entries which start with .
	-A	Like -a, but exclude . and ..
	-x	List by lines
	-d	List directory entries instead of contents
	-L	Follow symlinks
	-H	Follow symlinks on command line
	-R	Recurse
	-p	Append / to dir entries
	-F	Append indicator (one of */=@|) to entries
	-l	Long listing format
	-i	List inode numbers
	-n	List numeric UIDs and GIDs instead of names
	-s	List allocated blocks
	-lc	List ctime
	-lu	List atime
	--full-time	List full date and time
	-h	Human readable sizes (1K 243M 2G)
	--group-directories-first
	-S	Sort by size
	-X	Sort by extension
	-v	Sort by version
	-t	Sort by mtime
	-tc	Sort by ctime
	-tu	Sort by atime
	-r	Reverse sort order
	-w N	Format N columns wide
	--color[={always,never,auto}]	Control coloring
```

This is actually not the typically output of `ls --help`, and this is
because the `bash:5.1` docker image actually uses *BusyBox* under the
hood. The only thing to take away from that statement is that BusyBox is
another shell like BASH, though very minimal. Fortunately the BusyBox
`ls` command contains examples of both short and long options. The
following is the result of running `ls -lh`, which is the combination of
the `-l` (displays long format) and the `-h` (in long format listings,
display file sizes in human readable format) options.


```
total 56K    
drwxr-xr-x    1 root     root        4.0K Jan  6 20:20 bin
drwxr-xr-x    5 root     root         340 Jan 11 18:36 dev
drwxr-xr-x    1 root     root        4.0K Jan 11 18:36 etc
drwxr-xr-x    2 root     root        4.0K Nov 12 09:18 home
drwxr-xr-x    1 root     root        4.0K Jan  6 20:20 lib
drwxr-xr-x    5 root     root        4.0K Nov 12 09:18 media
drwxr-xr-x    2 root     root        4.0K Nov 12 09:18 mnt
drwxr-xr-x    2 root     root        4.0K Nov 12 09:18 opt
dr-xr-xr-x  313 root     root           0 Jan 11 18:36 proc
drwx------    2 root     root        4.0K Nov 12 09:18 root
drwxr-xr-x    2 root     root        4.0K Nov 12 09:18 run
drwxr-xr-x    2 root     root        4.0K Nov 12 09:18 sbin
drwxr-xr-x    2 root     root        4.0K Nov 12 09:18 srv
dr-xr-xr-x   13 root     root           0 Jan 11 18:36 sys
drwxrwxrwt    1 root     root        4.0K Jan  6 20:20 tmp
drwxr-xr-x    1 root     root        4.0K Jan  6 20:20 usr
drwxr-xr-x    1 root     root        4.0K Jan  6 20:20 var
```

When looking at a long listing format, it can be broken down like the
following.

* `drwxr-xr-x` is the access rights or permissions of the file. The
* initial character (`d`) indicates the type of the file. In this case
* "d" means a directory. We learn more about permissions later.
* `1` indicates the number of hard links. Links are explored more below.
* `root` part is the username of the file's owner.
* `root` part is the name of the group that owns the file.
* `0` or `4.0k` is the size of the file (in human readable format).
* `Nov 12 09:18` is the datetime of the last modification to the file.
* `bin` is the name of the file.

At first, `file` doesn't seem like that useful of a command, since all it
does is "Determine type of FILEs." For a programmer though, this
information is very useful, as it tells you things like if the program is
statically or dynamically linked. It also indicates things, like which C
library was used (`/lib/ld-musl-x86_64.so.1`), what CPU architecture the
program was compiled for (`x86-64`), and if debugging was removed
(`stripped`).

```
/usr/bin/file: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib/ld-musl-x86_64.so.1, stripped
```

The `less` command is one of a few that are used to output the contents
of a file. The following is the output of `less /etc/passwd`.

```
root:x:0:0:root:/root:/bin/ash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
halt:x:7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/mail:/sbin/nologin
news:x:9:13:news:/usr/lib/news:/sbin/nologin
uucp:x:10:14:uucp:/var/spool/uucppublic:/sbin/nologin
operator:x:11:0:operator:/root:/sbin/nologin
man:x:13:15:man:/usr/man:/sbin/nologin
postmaster:x:14:12:postmaster:/var/mail:/sbin/nologin
cron:x:16:16:cron:/var/spool/cron:/sbin/nologin
ftp:x:21:21::/var/lib/ftp:/sbin/nologin
sshd:x:22:22:sshd:/dev/null:/sbin/nologin
at:x:25:25:at:/var/spool/cron/atjobs:/sbin/nologin
squid:x:31:31:Squid:/var/cache/squid:/sbin/nologin
xfs:x:33:33:X Font Server:/etc/X11/fs:/sbin/nologin
games:x:35:35:games:/usr/games:/sbin/nologin
cyrus:x:85:12::/usr/cyrus:/sbin/nologin
vpopmail:x:89:89::/var/vpopmail:/sbin/nologin
ntp:x:123:123:NTP:/var/empty:/sbin/nologin
smmsp:x:209:209:smmsp:/var/spool/mqueue:/sbin/nologin
guest:x:405:100:guest:/dev/null:/sbin/nologin
nobody:x:65534:65534:nobody:/:/sbin/nologin
utmp:x:100:406:utmp:/home/utmp:/bin/false
```

Though `vim` has not been covered yet, `less` uses similar hotkeys (like
`j`/`k` to move up/down, or `/` to search.

Though the filesystem of the `bash:5.1` docker image is different, it
still contains most of the core directories that are found on any other
Unix-like system.

* `/` is the root directory
* `/bin` contains binaries required for the system to boot/run
* `/boot` contains the Linux kernel, initial RAM disk image, and the bootloader
* `/dev` contains *device nodes*
* `/etc` contains system-wide configuration files
* `/home` contains user directories in a normal setup
* `/lib` contains shared libraries
* `/lost+found` contains a partial recovery from a filesystem corruption
* `/media` (on modern Linux systems) contains mount points for *automatically* mounted devices
* `/mnt` (on older Linux systems) contains mount points for *manually*  mounted removable devices
* `/opt` contains "optionally" installed software
* `/proc` contains processes running on the system
* `/root` is the root account home directory
* `/sbin` contains "system" binaries which perform vital system tasks
* `/tmp` contains temporary/transient files
* `/usr` contains all programs and support files used by regular users
* `/usr/bin` contains the executable binaries installed by the Linux distribution
* `/usr/lib` contains shared libraries for programs in `/usr/bin`
* `/usr/local` contains binaries not installed by the Linux distribution, but are used system-wide
* `/usr/sbin` contains more system administration binaries
* `/usr/share` contains all shared data used by binaries in `/usr/bin`
* `/usr/share/doc` contains documentation included with packages
* `/var` contains data that is likely to change
* `/var/log` contains system log files

The last thing covered in this chapter are *links*. If we run the command
`ls -l /bin/sh`, we get the following.

```
lrwxrwxrwx    1 root     root            12 Nov 12 09:18 /bin/sh -> /bin/busybox
```

The key thing to note here is `/bin/sh -> /bin/busybox`. This is a
special kind of file called a *symbolic link* (also referred to as
*soft link* or *symlink*). This allows a file to be referenced by
multiple names, which comes in handy when you have different versions of
the same program. There is another type of link, called a *hard link*,
which is similar to a symbolic link, but they operate in different ways.
Links are covered more in the next chapter.

Related:

* TLCL
	<https://www.linuxcommand.org/tlcl.php/>

Tags:

	#tlcl #shell #unix
