# Learning Go With Tests (LGWT)

I was introduced to Go back in 2017, but still being a beginner and
learning Python3 at the time, I passed on it. Towards the middle of 2018,
I ended up picking up Go as I had ran into issues with Python's `GIL`
when creating a data collection web crawler component for an open source
AI/ML pipeline I was creating. This forced me to look for alternatives,
and fortunately I had been suggested Go by my good friend the year prior.

This lead me down the rabbit hole of learning about web crawling, search
engines, concurrency, and a lot of other really awesome topics. It also
lead me to learn Go (Goccer referenced below) by porting my Python3
program. You can still view the original Python3 project (Open Collection
or OC) referenced below.

The downside of learning this way, is that I missed out on learning very
important parts (like GoDoc) of the language early on, the biggest being
testing. Though I have picked up on pieces, there are various things that
I still need to properly learn.

Fortunately there is an awesome project called *Learn Go With Tests*,
which is a free and open source resource to (as the name implies) learn
Go through Test-Driven Development (TDD). I have always put off taking
the time to properly learn Go cause there are so many things that I want
to create and do *right now*. As part of my "Making Good Habits", I am
going back and re-learning Go from the ground up.

My reasoning for choosing this resource over others available, is because
this is the only one I've found that has a specific TDD approach.

If you are new to programming or are considering learning Go for whatever
reason, I encourage you to write your own, but below is an example of a
simple Go program/test. If you are wondering *why tests are necessary*,
then imagine maintaining/debugging a medium to large codebase. For a
concrete example, put yourself in the perspective of a web developer. One
common aspect of websites are web forms, which are a component that
introduces functionality that can fail. Manual testing of things like
forms becomes time consuming, and so the better option is to write a test
and run it whenever a change is introduced.

```Go
// main.go
package main

import "fmt"

func PrintHelloWorld() string {
	return "hello, world!"
}

func main() {
	fmt.Println(PrintHelloWorld())
}
```

```Go
// main_test.go
package main

import "testing"

func TestPrintHelloWorld(t *testing.T) {
	expected := "hello, world!"
	actual := PrintHelloWorld()

	if actual != expected {
		t.Errorf("\nExpected: %s\nActual: %s", expected, actual)
}
```

Related:

* Python's GIL
	<https://wiki.python.org/moin/GlobalInterpreterLock>
* Open Collection (OC)
	<https://github.com/oglinuk/oc>
* Goccer
	<https://github.com/oglinuk/goccer>
* Learn Go With Tests
	<https://github.com/quii/learn-go-with-tests>
* Go `testing`
	<https://pkg.go.dev/testing>

Tags:

	#go #tdd #python-gil #testing
