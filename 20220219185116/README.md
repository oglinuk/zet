# Automation: `entr` - Event Notify Test Runner

"A utility for running arbitrary commands when files change. Uses
kqueue(2) or inotify(7) to avoid polling. entr was written to make rapid
feedback and automated testing natural and completely ordinary."

Example use case: Golang testing

`ls *.go | entr go test`

Related:

* `entr`
	<https://github.com/eradman/entr>

Tags:

	#automation #c #testing #inotify #kqueue #event-driven
