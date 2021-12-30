# TIL `for(int i = 0; s[i]; i++)` in C

Iteration is something done all the time in programming, especially over
array types. To iterate over an array, you need to know it's size or how
many elements the array contains. My normal approach to this in C would
be to use `strlen`, as `sizeof` runs into issues with pointer decay.

After reading Ken Thompsons paper "Reflections on Trusting Trust", as a
challenge I re-implemented the program shown in Figure 1. The way his
program iterates through an array doesn't use `strlen` or `sizeof` to
calculate the size of the array. A simple hello world program example
using this method looks like the following.

```C
#include <stdio.h>

void f(char s[])
{
	for (int i = 0; s[i]; i++)
		printf("%c", s[i]);
}

int main()
{
	char s[] = {'h','e','l','l','o',',',' ','w','o','r','l','d','!',10,0};
	f(s);
	return 0;
}
```

What is so great about this way of iterating is, not only does it handle
pointer decay, but there is no need for `<string.h>`. Now I am wondering
what are the cases you would want to use another approach of iterating
than the one above. TODO: Confirm with a more experienced C programmer.

How it works is explained in section `6.8.5 Iteration statments`, part 4
under `Semantics` in the C programming language international standard.

Related:

* C Programming Language International Standard
	<https://web.archive.org/web/20111224141940/http://www.open-std.org/jtc1/sc22/wg14/www/docs/n1570.pdf>
* Ken Thompsons paper "Reflections on Trusting Trust"
	<https://github.com/oglinuk/ken-thompsons-rott-quine/blob/master/rott.pdf>

Tags:

	#c #ken-thompson #iteration
