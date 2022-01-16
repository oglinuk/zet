# TLCL: 4 - Manipulating Files and Directories

This chapter introduces the concept of wildcards (globbing), along with
the `cp`, `mv`, `mkdir`, `rm`, and `ln` commands.

A *wildcard* in Unix-like systems is a special character that allows for
the specification of a certain filename. It is easier to show than
explain.

Let's say we had a directory full of `.txt` files and we wanted to move
them all to the parent directory using the shell. With the `mv` command,
we can enter each file in the command and execute it to move all files.
Fortunately there is a better way via the use of wildcards (the use of a
wildcard is called *globbing*). The `*` wildcard matches any characters,
so we can run a command like `mv *.txt ..`.

Below is a list of wildcards:

* `*` matches any characters
* `?` matches any single character
* `[chars]` matches any character that is a member of the set *chars*
* `[!chars]` matches any character that is not a member of the set *chars*
* `[[:class:]]` matches any character that is a member of the specified *class*

Below is a list of commonly used character classes:

* `[:alnum:]` matches any alphanumeric character
* `[:alpha:]` matches any alphabetic character
* `[:digit:]` matches any numeral
* `[:lower:]` matches any lowercase letter
* `[:upper:]` matches any uppercase letter

Below is a list of examples:

* `*` matches all files
* `a*` matches all files beginning with `a`
* `a*.txt` matches all files beginning with `a` and ending with `.txt`
* `sys???` matches all files beginning with `sys`, followed by exactly three characters
* `[tuv]` matches all files beginning with either `t`, `u`, or `v`
* `log[0-9][0-9]` matches all files beginning with `log`, followed by exactly three numerals
* `[[:digit:]]*` matches all files beginning with a numeral
* `[![:upper:]]*` matches all files that do not begin with an uppercase letter
* `*[[:lower:]42]` matches all files ending with a lowercase letter or the numeral `4` or `2`

The `mkdir` command is used to create one or more directories (if the do
not exist). The command `mkdir bob alice elliot` creates the directories
`bob`, `alice`, and `elliot`. A useful option of the `mkdir` command is
the `-p` option, which allows for `mkdir -p `bob/alice/elliot`. This will
create all non-existent parent directories.

The `cp` command is used to copy one or more files/directories. It is
important to remember, that unlike the `mkdir` command, copying will
overwrite the destination if it exists. Similar to the `mkdir` command,
we can pass multiple items which will all be copied. A useful option
provided by the `cp` command, is the `-u` or `--update` option. This
option only copies files that don't exist or are newer than the existing
file in the destination directory.

The `mv` command is used for both moving and renaming files. Like the
`cp` command, it is important to remember that the `mv` command will
overwrite the destination if it exists. Also like the `cp` command, a
useful option for the `mv` command is the `-u` or `--update` option,
which only moves files that either don't exist or are newer. Another
useful option is `-i` or `--interactive`, which prompts for confirmation
before overwriting an existing file.

The `rm` command is used to remove/delete files. This is the most
dangerous command, and should be used with caution. It is dangerous,
because the `rm` command does not send the removed file(s) to the trash,
but removes it entirely from the system. Like the `mv` command, the `rm`
command has the `-i` or `--interactive` option, which prompts the user
for confirmation before deleting file(s). Another useful option is the
`-f` or `--force`, which ignores nonexistent files/arguments and
overrides the prompt from the `-i`/`--interactive` option.

The `ln` command is used to create hard/symbolic links. Every file has a
single hard link, which is what gives the file it's name.

Hard links are two limitations that are important to remember.

1. A hard link is not able to reference a file outside its own filesystem
1. A hard link is not able to reference a directory

Symbolic links came about to overcome the limitations of hard links, by
creating a special type of file that contains a text pointer to the
referenced file(s).

Related:

* TLCL
	<https://www.linuxcommand.org/tlcl.php/>

Tags:

	#tlcl #shell
