# Code Sprint 1642914462: `init`

The first warning from `shellcheck` is `SC2164`, which states that "`cd`
can fail for a variety of reasons: misspelled paths, missing directories,
missing permissions, broken symlinks and more. To avoid this, make sure
you handle the cases when `cd` fails."

The second warning from `shellcheck` is `SC2048`, which states "`$*` and
`${array[*]}`, unquoted, is subject to word splitting and globbing."

Next to replace the two relative paths (`./cmd/api` and `./cmd/ui`) with
absolute paths (`"$PWD/cmd/api"` and `"$PWD/cmd/ui"`).

Finally to add tab-completion using the built-in programmable completion
of BASH. My knowledge is limited, but I will draw from rwxrobs "Use
`build` Shell Script Instead of `make`". We first create an environment
variable called `cmds` with the function names space delimited. Next we
check to see if the length of `COMP_LINE` is non-zero via `-n`. If it is,
then create an environment variable called `cl` which is the result of a
parameter expansion using `##* `, which applies the pattern removal
operation on every parameter. In this case the pattern is a space. Then
for each `c`ommand in `cmds`, run `test` with two checks. The first check
is to see if the length of `cl` is zero. The `-o` option specifies
"either EXPRESSION1 or EXPRESSION2 is true". The second check is if `c`
matches the result of a parameter expansion using `#`, which removes the
first matching case using `cl` for the pattern. If either of these checks
are satisfied, then `echo` the value of `c`.

We can now run `complete -C ./init ./init` and tabbing after typing
`./init` gives the following output.

```BASH
api       app       clean     dapi      dclean    dcompose  ui
```

`./init a` gives

```BASH
api  app
```

One thing I added to `init clean` which `shellcheck` doesn't care about
is the use of `rm` without the `-i` option. This is just so that the user
is prompted before every removal in case they want to keep any of the
files.

Related

* Shellcheck `SC2164`
	<https://github.com/koalaman/shellcheck/wiki/SC2164>
* Shellcheck `SC2048`
	<https://github.com/koalaman/shellcheck/wiki/SC2048>
* BASH Programmable completion (`man bash`)
* `test` (`man test`)
* Rwxrob's "Use `build` Shell Script Instead of `make`" zet
	<https://github.com/rwxrob/zet/tree/0e8e644958873d88f1ffa17fe3e2e9b4d4505bac/20210521134814>
