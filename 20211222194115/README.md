# RGB Feature Scaling in C

Feature scaling is used to scale values to a range between 0 and 1. The
equation is `n = a + (a - min(x)/(max(x) - min(x)))`. Since RGB values
deal with a min of `0` and a max of `255` this makes the equation
`normalized = a / 255`.

The context for this is because my `dasteroids` project uses the allegro
game libraries, and the function I use to create an `ALLEGRO_COLOR` is
`al_map_rgb_f`, which takes three floats from 0 to 1.

If I want to create the color red then the corresponding call would be
`al_map_rgb_f(1.0, 0.0, 0.0);`, but if I want to create the color orange
(255, 127, 0), I would need to normalize `127`. Using the above equation,
the normalized value is `127/255`, which is `0.498039`.

The implementation in C looks like the following.

```C
#include <stdio.h>
#include <stdlib.h>

int main(int argc, const char* argv[])
{
	if (argc < 2) {
		printf("Usage: ./main <0-255>\n");
		exit(-1);
	}

	char *endptr;
	float n = strtof(argv[1], &endptr);

	float normalized = n / 255.0;

	printf("%f normalized: %f\n", n, normalized);

	return 0;
}
```

and when running `./main 42`, we get `42.000000 normalized: 0.164706`.

Related:

* <https://github.com/oglinuk/dasteroids>
* <https://github.com/liballeg/allegro5>
* <https://liballeg.org/a5docs/trunk/graphics.html#al_map_rgb_f>
* `man strtof`

Tags:

	#c #feature-scaling
