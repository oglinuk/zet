# TLCL: 1 - What is the Shell?

You often hear the terms "shell" and "terminal" when the topic is about
Linux.

A *shell*, is "the command interpreter used to pass commands to an
operating system; so called because it is the part of the operating
system that interfaces with the outside world." Some spelunking resulted
in a post by IBM, titled "A history of shells", which states "shells - or
*command-line interpreters* - have a long history, but this discussion
begins with the first UNIX shell. Ken Thompson (of Bell Labs) developed
the first shell for UNIX called the *V6 shell* in 1971." The post goes on
to state "what the Thompson shell lacked was the ability to script." I
won't quote anymore, so that the reader is inclined to go read the
article.

A *terminal* is much more complicated and has a much longer history.
First, it's important to clarify that when you hear "terminal", people
are actually referring to a *terminal emulator*. The term terminal comes
from a much older technology, the *teletype*. Though I will not cover TTY
or it's history in this zet, I have added a link to a great article
below. All you need to know is that a terminal emulator is a piece of
software that emulates a terminal. This is what allows a user to interact
with a shell.

If we bring up a terminal via `ctrl + alt + t`, we are brought to a
*shell prompt*, which means the shell is ready to accept input. The shell
prompt will look different, but will usually display
*username@machinename*. If the last character in the shell prompt is a
`#` rather than a `$`, it means the terminal session has *superuser*
privileges.

Typing in some garbage (`thisisgarbage`), results in `thisisgarbage:
command not found`. This is is known as *garbage-in, garbage-out (GIGO)*.
Typing in a known command (like `date`), will execute the command (and
produce output if any).

We have access to a history of all the commands ran (up to the last 1000
commands by default usually), by either typing `history`, pressing the
up-arrow/down-arrow keys, or `ctrl + [` and `j`/`k` (if `set -o vi` is
enabled).

One important thing to remember with terminal emulators is how to copy
and paste. The primary way is `ctrl + alt + c` and `ctrl + alt + v`, but
you can also copy things by highlighting with your mouse and pasting by
the middle mouse button. Keep in mind that they use different buffers
though, so what you copy with `ctrl + alt + c` will not be able to be
pasted via the middle mouse click.

The first commands introduced are `date`, `cal`, `df`, and `free`.

The `date` command prints the current datetime (`Mon 10 Jan 2022 09:48:59 AM
PST`).

The `cal` command prints a calendar (the current month by default).

```
    January 2022      
Su Mo Tu We Th Fr Sa  
                   1  
 2  3  4  5  6  7  8  
 9 10 11 12 13 14 15  
16 17 18 19 20 21 22  
23 24 25 26 27 28 29  
30 31                 
```

The `df` command prints disk space usage.

```
Filesystem           1K-blocks      Used Available Use% Mounted on
overlay              114337956  93153308  15333512  86% /
tmpfs                    65536         0     65536   0% /dev
tmpfs                  4010568         0   4010568   0% /sys/fs/cgroup
shm                      65536         0     65536   0% /dev/shm
/dev/sda2            114337956  93153308  15333512  86% /etc/resolv.conf
/dev/sda2            114337956  93153308  15333512  86% /etc/hostname
/dev/sda2            114337956  93153308  15333512  86% /etc/hosts
tmpfs                  4010568         0   4010568   0% /proc/asound
tmpfs                  4010568         0   4010568   0% /proc/acpi
tmpfs                    65536         0     65536   0% /proc/kcore
tmpfs                    65536         0     65536   0% /proc/keys
tmpfs                    65536         0     65536   0% /proc/timer_list
tmpfs                    65536         0     65536   0% /proc/sched_debug
tmpfs                  4010568         0   4010568   0% /proc/scsi
tmpfs                  4010568         0   4010568   0% /sys/firmware
```

The `free` command prints memory usage.

```
              total        used        free      shared  buff/cache available
Mem:        8021140     1351760     3456164      322484     3213216 	6071500
Swap:       2097148         900     2096248
```

It is important to note that I used a docker container, running the
`bash:5.1` docker image, to run the above commands.

To end a terminal session, you can either enter `exit`, or you can enter
`ctrl + d`.

The last thing covered in this chapter is *virtual terminals* or *virtual
consoles*. These are terminal sessions that continue to run in the
background, even when there is no terminal emulator running. To access a
virtual terminal, enter `ctrl + alt + F1` through `ctrl + alt + F6`. You
can swap between virtual terminals via `alt + F1` through `alt + F6`.
Typically to return to the graphical desktop, enter `alt + F7`.

Related:

* TLCL
	<https://www.linuxcommand.org/tlcl.php/>
* Shell
	<https://web.archive.org/web/20031117173334/http://www.catb.org/jargon/html/S/shell.html>
* Evolution of shells in Linux
	<https://web.archive.org/web/20190423054159/https://developer.ibm.com/tutorials/l-linux-shells/>
* The TTY demystified
	<https://web.archive.org/web/20090619112251/https://www.linusakesson.net/programming/tty/>

Tags:

	#tlcl #shell #terminal #tty #bash
