# Go vs Rust vs Insert Language Here

Programming language wars have been waged for a long time. I was
fortunate to understand early on that the language you use is arbitrary,
it is the problem that matters. You will often hear the phrase "use the
right tool for the job", and this applies with programming languages.

In my opinion, you cant be a programmer in todays world without having
knowledge of at least a second or third language. The reason I say 
this, is because there will be some cases where a language doesnt make
sense. For example you would not want to use C/C++ for a REST API, or
interpreted languages when speed is a concern.

The question then shifts to "when do you know which language to use
when?", and the answer to that comes with experience. The quickest way to
get this experience is to implement common programs (such as a
calculator, guessing game, typing practice game, website, ...) in the
languages you are wondering about.

For example in my case, I started to learn Rust because I wanted to see
if it would be a better option for a web crawling library than Go. After
implementing a concurrent web crawler in Rust, I realized how much
different the functional programming paradigm is. Since the difference is
so great, and the cases where I would use Rust are so little, I chose to
stick with Go.

Related:

* Concurrent Go crawler
	<https://github.com/oglinuk/goccer>
* Concurrent Rust crawler
	<https://github.com/oglinuk/cruster>

Tags:

	#go #rust #language-wars
