# Reflections on Trusting Trust by Ken Thompson

Wow. If I had to sum up this paper in one word, that would be it. Ken
Thompson is already a legendary person to me because of his work on
things like C, but this paper has changed my perspective of software
forever. To give some context, this paper was for as far as I understand,
a lecture given as the co-recipient of the Turing Award.

The paper "Reflections on Trusting Trust" is only *three pages* and
starts off by stating "To what extent should one trust a statement that a
program is free of Trojan horses? Perhaps it is more important to trust
the people who wrote the software." If you don't know what a Trojan horse
is in a computer science context, then just understand it is malicious.
To put this statement into perspective, think about how many programs you
have installed in the past, each time *trusting* the programmer(s) that
it wasn't malicious. Everytime you install a piece of software, think of
this statement.

Ken breaks this experiment down into three stages.

In the stage I, he describes how in his college days, one of their
favorite programming exercises was writing the shortest self-reproducing
program. "More precisely stated, the problem is to write a source program
that, when compiled and executed, will produce as output an exact copy of
its source. If you have never done this, I urge you to try it on your
own. The discovery of how to do it is a revelation that far surpasses any
benefit obtained by being told how to do it. The part about 'shortest'
was just an incentive to demonstrate skill and determine a winner." Below
is an example implementation of a self-reproducing program in Go.

```Go
package main

import "fmt"

// Go is easier since it has [raw string literals](https://go.dev/ref/spec#String_literals),
// the work-around to not being able to use '`' is the same as '"'.
func main() {
	s := `package main

import "fmt"

// Go is easier since it has [raw string literals](https://go.dev/ref/spec#String_literals),
// the work-around to not being able to use '%c' is the same as '"'.

func main() {
	s := %c%s%c
	fmt.Printf(s, rune(96), rune(96), s, rune(96))
}
`
	fmt.Printf(s, rune(96), rune(96), s, rune(96))
}
```


Stage II describes how compilers written in their own languages (like
the C compiler) are "chicken and egg" problems. This problem introduces
another problem where you can compile/distribute a tampered compiler
binary. To understand why this is a problem, you have to think about how
you would try to solve it. If the compiler is tampered with, how could
you compile a new compiler with the necessary fixes?

Stage III describes how the C compiler can be modified to implement a
Trojan horse, but also a real world example. "The actual bug I planted in
the compiler would match code in the UNIX 'login' command. The
replacement code would miscompile the login command so that it would
accept either the intended encrypted password or a particular known
password. Thus if this code were installed in binary and the binary were
used to compile the login command, I could log into that system as any
user." If you think that is bad, *it get's worse*.

"Such blatant code would not go undetected for long. Even the most casual
perusal of the source of the C compiler would raise suspicions. The final
step is represented in Figure 3.3. This simply adds a second Trojan horse
to the one that already exists. The second pattern is aimed at the C
compiler. The replacement code is a Stage I self-reproducing program that
inserts both Trojan horses into the compiler. This requires a learning
phase as in the Stage II example. First we compile the modified source
with the normal C compiler to produce a bugged binary. We install this
binary as the official C. We can now remove the bugs from the source of
the compiler and the new binary will reinsert the bugs whenever it is
compiled. Of course, the login command will remain bugged with no trace
in source anywhere."

That is the stuff of nightmares.

For a distraction from your now endless void of despair thinking about
how you will now traverse the future knowing of the Ken Thompson hack, I
re-created the self-reproducing program shown in Figure 1.

```C
char s[] = {
	'\t',
	'0',
	'\n',
	'}',
	';',
	'\n',
	'\n',
	'/',
	'*',
	'\n',
	' ',
	'*',
	' ',
	'T',
	'h',
	'e',
	' ',
	's',
	't',
	'r',
	'i',
	'n',
	'g',
	' ',
	's',
	' ',
	'i',
	's',
	' ',
	'a',
	'\n',
	' ',
	'*',
	' ',
	'r',
	'e',
	'p',
	'r',
	'e',
	's',
	'e',
	'n',
	't',
	'a',
	't',
	'i',
	'o',
	'n',
	' ',
	'o',
	'f',
	' ',
	't',
	'h',
	'e',
	' ',
	'b',
	'o',
	'd',
	'y',
	'\n',
	' ',
	'*',
	' ',
	'o',
	'f',
	' ',
	't',
	'h',
	'i',
	's',
	' ',
	'p',
	'r',
	'o',
	'g',
	'r',
	'a',
	'm',
	' ',
	'f',
	'r',
	'o',
	'm',
	' ',
	'\'',
	'0',
	'\'',
	'\n',
	' ',
	'*',
	' ',
	't',
	'o',
	' ',
	't',
	'h',
	'e',
	' ',
	'e',
	'n',
	'd',
	'.',
	'\n',
	' ',
	'*',
	'/',
	'\n',
	'\n',
	'm',
	'a',
	'i',
	'n',
	'(',
	')',
	'\n',
	'{',
	'\n',
	'\t',
	'i',
	'n',
	't',
	' ',
	'i',
	';',
	'\n',
	'\n',
	'\t',
	'p',
	'r',
	'i',
	'n',
	't',
	'f',
	'(',
	'"',
	'c',
	'h',
	'a',
	'r',
	'\\',
	't',
	's',
	'[',
	']',
	' ',
	'=',
	' ',
	'{',
	'\\',
	'n',
	'"',
	')',
	';',
	'\n',
	'\t',
	'f',
	'o',
	'r',
	' ',
	'(',
	'i',
	' ',
	'=',
	' ',
	'0',
	';',
	' ',
	's',
	'[',
	'i',
	']',
	';',
	' ',
	'i',
	'+',
	'+',
	')',
	'\n',
	'\t',
	'\t',
	'p',
	'r',
	'i',
	'n',
	't',
	'f',
	'(',
	'"',
	'\\',
	't',
	'%',
	'd',
	',',
	' ',
	'\\',
	'n',
	'"',
	',',
	' ',
	's',
	'[',
	'i',
	']',
	')',
	';',
	'\n',
	'\t',
	'p',
	'r',
	'i',
	'n',
	't',
	'f',
	'(',
	'"',
	'%',
	's',
	'"',
	',',
	' ',
	's',
	')',
	';',
	'\n',
	'}'
};

/*
 * The string s is a
 * representation of the body
 * of this program from '0'
 * to the end.
 */

main()
{
	int i;

	printf("char\ts[] = {\n");
	for (i = 0; s[i]; i++)
		printf("\t%d, \n", s[i]);
	printf("%s", s);
}
```

Related:

* Reflections on Trusting Trust (paper)
	<https://web.archive.org/web/20191203212005/https://www.cs.cmu.edu/~rdriley/487/papers/Thompson_1984_ReflectionsonTrustingTrust.pdf>
* Implementation of Ken Thompsons Quine in C source code
	<https://github.com/oglinuk/ken-thompsons-quine-in-c>
* Reflections on Trusting Trust (computerphile video explanation)
	<https://www.youtube.com/watch?v=SJ7lOus1FzQ>
