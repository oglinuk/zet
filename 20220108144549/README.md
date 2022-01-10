# Understanding the Unix Philosophy

If you know about Unix, then you most likely know about it's famous
philosophy. Until now I have never applied the rwx method and truly
understood it.

After some initial spelunking, I found the first instance of the Unix
philosophy, documented by Douglas McIlroy in "Unix Time-Share System:
Forward".

```
(i) Make each program do one thing well. To do a new job, build afresh
rather than complicate old programs by adding new "features."

(ii) Expect the output of every program to become the input to another,
as yet unknown, program. Don't clutter output with extraneous
information. Avoid stringently columnar or binary input formats. Don't
insist on interactive input.

(iii) Design and build software, even operating systems, to be tried
early, ideally within weeks. Don't hesitate to throw away the clumsy
parts and rebuild them.

(iv) Use tools in preference to unskilled help to lighten a programming
task, even if you have to detour to bulid the tools and expect to throw
some of them out after you've finished using them.
```

Let's create a small example in BASH to reflect the above 4 axioms. 

```BASH
#!/bin/bash

while IFS= read line; do
	echo "${line^^}"
done
```

This small utility reads from stdin and outputs an uppercase version of
the read line via BASH parameter expansion.

```
hello,
world!
```

If we pass a file (called `lower.txt`) with the data above to our script
(called `toupper`) using redirection (`./toupper < lower.txt`), we get
the following result.

```
HELLO,
WORLD!
```

We can also use this small utility in combination with another like
`find`. This might look like `find /usr/include std* | ./toupper`.

Another great documented instance of the Unix philosophy is by one of the
core people behind the open source movement, Eric S. Raymond. He lists 12
rules that he states were "implied not by what these elders said but by
what they did and the example Unix itself set."

```
1. Rule of Modularity: Write simple parts connected by clean interfaces.
2. Rule of Clarity: Clarity is better than cleverness.
3. Rule of Composition: Design programs to be connected to other programs.
4. Rule of Separation: Separate policy from mechanism; separate interfaces from engines.
5. Rule of Simplicity: Design for simplicity; add complexity only where you must.
6. Rule of Parsimony: Write a big program only when it is clear by demonstration that nothing else will do.
7. Rule of Transparency: Design for visibility to make inspection and debugging easier.
8. Rule of Robustness: Robustness is the child of transparency and simplicity.
9. Rule of Representation: Fold knowledge into data so program logic can be stupid and robust.
10. Rule of Least Surprise: In interface design, always do the least surprising thing.
11. Rule of Silence: When a program has nothing surprising to say, it should say nothing.
12. Rule of Repair: When you must fail, fail noisily and as soon as possible.
13. Rule of Economy: Programmer time is expensive; conserve it in preference to machine time.
14. Rule of Generation: Avoid hand-hacking; write programs to write programs when you can.
15. Rule of Optimization: Prototype before polishing. Get it working before you optimize it.
16. Rule of Diversity: Distrust all claims for "one true way".
17. Rule of Extensibility: Design for the future, because it will be here sooner than you think.
```

Related:

* Unix Time-Share System: Forward by Douglas McIlroy
	<https://archive.org/details/bstj57-6-1899/page/n3/mode/2up>
* `man bash` and search "Parameter Expansion"
* Basics of the Unix Philosophy by Eric S. Raymond
	<https://web.archive.org/web/20030425025631/http://www.catb.org/~esr/writings/taoup/html/ch01s06.html>
