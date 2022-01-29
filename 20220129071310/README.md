# Quines: More Than Just Outputting Source Code

I can't remember who exactly from the community it was, but I was first
introduced to Quines through someone mentioning the 128 Ouroborous
Quine. If you do what I did and search the term "Quine", then looked at
the wikipedia page, you will get the definition "a computer program which
takes no input and produces a copy of its own source code as its only
output." A reason you should never rely on the wikipedia page itself, but
rather the sources they refence is with the definition just given. In the
referenced paper by Ken Thompson, there is no mention of requiring that
the program "takes no input".

If you browse the references and further reading sections, you might come
across the link to Ken Thompson's paper "Reflections on Trusting Trust".
For context, Ken Thompson is one of the creators of the C programming
language and modern Unix. This paper is only three pages long, but is
very technical. I wont cover it in this zet, as I have already done a
breakdown of it in a previous one referenced below. To summerize and give
an overview, Quines are a component used in malware to replicate.

After readying his paper and implementing his original Quine in C, I
began tinkering around with Quines in Go. Fortunately, Go makes writing
Quines super easy with string literals and runes. The first thing I
wanted to do after figuring out a basic Quine, was create a Quine that
compiled itself. Go again makes this easy, this time with the `os/exec`
package from the standard library.

My first implementation of a self-compiling Go Quine is 55 lines and
looks like the following.

```Go
package main

import (
	"fmt"
	"os"
	"os/exec"
)

func main() {
	s := `package main

import (
	"fmt"
	"os"
	"os/exec"
)

func main() {
	s := %c%s%c

	os.Remove("go.mod")

	p, _ := exec.LookPath("go")
	modInit := &exec.Cmd{
		Path: p,
		Args: []string{p, "mod", "init", "example.com/self-compiling"},
	}
	_ = modInit.Run()

	build := &exec.Cmd{
		Path: p,
		Args: []string{p, "build", "-o", "self"},
	}
	_ = build.Run()

	fmt.Printf(s, rune(96), s, rune(96))
}
`
	os.Remove("go.mod")

	p, _ := exec.LookPath("go")
	modInit := &exec.Cmd{
		Path: p,
		Args: []string{p, "mod", "init", "example.com/self-compiling"},
	}
	_ = modInit.Run()

	build := &exec.Cmd{
		Path: p,
		Args: []string{p, "build", "-o", "self"},
	}
	_ = build.Run()

	fmt.Printf(s, rune(96), s, rune(96))
}
```

There is actually an additional thing happening to self-compiling, which
is generating a Go module. Modules have been required since Go 1.16, and
we leverage `os/exec` yet again to handle the module creation. If you
want to play around with the above example, one way you can do in a
terminal is `go run main.go > valid.go && go run valid.go`.

The next step after self-compiling was figuring out how to self-modify.

I won't post the entire program as it is 126 lines of code, but below is
the function that contains the self-modification logic.

```Go
var (
	mods = []string {
		"fmt.Fprintf(os.Stderr, %chello, world self-modification one!%c%c%c)",
		"fmt.Fprintf(os.Stderr, %chello, world self-modification two!%c%c%c)",
		"fmt.Fprintf(os.Stderr, %chello, world self-modification three!%c%c%c)",
	}
)

func f() {
	fmt.Fprintf(os.Stderr, "hello, world!")
	old, _ := os.Open("main.go")
	defer old.Close()

	me, _ := os.Create("new.go")
	defer me.Close()

	bs := bufio.NewScanner(old)
	for bs.Scan() {
		me.WriteString(fmt.Sprintf("%s\n", bs.Text()))
		if bs.Text() == "func f() {" {
			me.WriteString(fmt.Sprintf("\t%s\n",fmt.Sprintf(mods[rand.Int()%len(mods)],rune(34),rune(92),rune(110),rune(34))))
		}
	}
	os.Rename("new.go", "main.go")
}
```

It won't make sense unless you go view the all the source code, but to
give you a hint, where I put `f` is key.

The latest Quine implementation is a type of Quine I am calling a
*Frankenquine*, since the idea behind it is a Quine that constructs
another program using various parts of either it's source code or source
code of the language used. Like the above program, the first Frakenquine
implementation is too large (192 lines) to stick in this zet.

This brings me to the spelunking session of searching for existing Quine
implementations to get inspiration for other types of Quines. Though
there were a lot of Quines that fall under the basic Quine type, I did
manage to find four notable Quines. I've refenced all four below, but
want to talk about one in particular.

`quinesnake` is what I consider to be a holy grail. Before you continue
reading, please take a moment to consider the scope of making the game of
snake. It requires graphics, a moving pixel that grows every time it goes
over a randomly placed "fruit", game lose when you hit a wall, and the
ability to move in the north, east, south, and west directions.

The source code (compact to one line) is 28 lines long, and looks like
the following. Below that is the running game.

```BASH
/*bin/ls>/dev/null;sed -n 's/.*.\/\*\(.*\)../\1/p' $0|I=$0 sh;exit;*/std::map<I,
I>m={{97,1},{'w',/*echo g++ -std=c++11 -oo $I -lcurses -DI=int -DF=if -DK=ret\*/
2},{'d',3}};I/*urn -includectime,curses.h,iostream,map,unistd.h|sed s/,/\ -in\*/
w=80,h=28,x=2,y=2,a=2,b=0,d,e,z=768;std::wstring/*clude/g|sh;./o</dev/tty;exit*/
s=LR"x(/*bin/ls>/dev/null;sed -n 's/.*.\/\*\(.*\)../\1/p' $0|I=$0 sh;exit;*/std:
:map<I,I>m={{97,1},{'w',/*echo g++ -std=c++11 -oo $I -lcurses -DI=int -DF=if -DK
=ret\*/2},{'d',3}};I/*urn -includectime,curses.h,iostream,map,unistd.h|sed s/,/\
 -in\*/w=80,h=28,x=2,y=2,a=2,b=0,d,e,z=768;std::wstring/*clude/g|sh;./o</dev/tty
;exit*/s=LR"x%dx";I G(I x,I y){K 3&s[y*w+x]>>8;}I C(I x,I y,I c){(s[y*w+x]&=~z)|
=c<<8;}I P(I d,I &x,I &y){F(d==1)x-=2;!d&&y++;d==2&&y--;F(d==3)x+=2;}I M(){curs_
set(0);I a=rand()%w/2*2,b=rand()%h;timeout(0);F(!G(a,b))C(a,b,2);else M();}I A(I
 x,I y){K s[y*w+x]>>10;}I S(I d){(s[y*w+x]&=~3072)|=d<<10;}I T(){d=A(x,y);F(0<=(
e=getch())&&abs(m[e]-d)!=2)d=m[e];S(d);P(d,x,y);F(x<0||y==h||y<0||x>w-2||G(x,y)&
1)K 0;S(d);F(G(x,y)&2)M();else{s[b*w+a]&=~z;P(A(a,b),a,b);}C(x,y,1);move(0,0);fo
r(I i=0;i<w*h;){attron(e=z&s[i]);addch((char)s[i++]);addch(s[i++]);attroff(e);F(
!(i%w))addch(10);}refresh();K 1;}I main(){srand(time(0));while((e=s.find(10))>0)
s.erase(e,1);s.replace(s.find(L"%d"),2,L"("+s+L")");initscr();start_color();for(
e=0;e<3;){init_pair(e,0,e+9);C(2,e++,1);}noecho();M();while(T())usleep(z<<7);end
win();})x";I G(I x,I y){K 3&s[y*w+x]>>8;}I C(I x,I y,I c){(s[y*w+x]&=~z)|=c<<8;}
I P(I d,I &x,I &y){F(d==1)x-=2;!d&&y++;d==2&&y--;F(d==3)x+=2;}I M(){curs_set(0);
I a=rand()%w/2*2,b=rand()%h;timeout(0);F(!G(a,b))C(a,b,2);else M();}I A(I x,I y)
{K s[y*w+x]>>10;}I S(I d){(s[y*w+x]&=~3072)|=d<<10;}I T(){d=A(x,y);F(0<=(e=getch
())&&abs(m[e]-d)!=2)d=m[e];S(d);P(d,x,y);F(x<0||y==h||y<0||x>w-2||G(x,y)&1)K 0;S
(d);F(G(x,y)&2)M();else{s[b*w+a]&=~z;P(A(a,b),a,b);}C(x,y,1);move(0,0);for(I i=0
;i<w*h;){attron(e=z&s[i]);addch((char)s[i++]);addch(s[i++]);attroff(e);F(!(i%w))
addch(10);}refresh();K 1;}I main(){srand(time(0));while((e=s.find(10))>0)s.erase
(e,1);s.replace(s.find(L"%d"),2,L"("+s+L")");initscr();start_color();for(e=0;e<3
;){init_pair(e,0,e+9);C(2,e++,1);}noecho();M();while(T())usleep(z<<7);endwin();}
```

![snakequine](https://raw.githubusercontent.com/taylorconor/quinesnake/master/animation.gif)

I hope you now share in my view that a Quine is so much more than just a
program that outputs it's own program.

Related:

* 128 Language Quine Relay
	<https://github.com/mame/quine-relay>
* Reflections on Trusting Trust by Ken Thompson zet
	<https://github.com/oglinuk/zet/tree/master/20211228062739>
* A collection of Quines
	<https://github.com/oglinuk/quines>
* Frankenquine
	<https://github.com/oglinuk/quines/blob/master/frankenquine/traditional/go/hello-world-go/main.go>
* snakequine
	<https://github.com/taylorconor/quinesnake>
* quinedb (pure BASH4 quine-based key-value db)
	<https://github.com/gfredericks/quinedb>
* self-replicating, self-modifying Assembly quine
	<https://github.com/mertyildiran/ldca>
* an HTML file that prints itself out in Star Wars opening style
	<https://github.com/miguel-sc/QuineWars>

Tags:

	#quines #c #go #bash #c++ #asm #ruby #rott
