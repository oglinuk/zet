# Code Sprint 1642914462: `cmd/ui`

Since there was only one thing TODO in `cmd/api`, I'm including it in
this patch. The only thing was to change from

```Go
import (
	"github.com/oglinuk/restful-go/internal/api"`
)
```

to  `import "github.com/oglinuk/restful-go/internal/api"`, since there is
only one import statement.

Refactoring `cmd/ui/Dockerfile` to a multi-stage build looks like the
following.

```Dockerfile
FROM golang:1.17 as build
WORKDIR /go/src/github.com/oglinuk/restful-go/ui
COPY . .
RUN go mod download && go mod verify
ENV CGO_ENABLED=0
RUN go build -ldflags="-w -s"

FROM scratch
COPY --from=build /go/src/github.com/oglinuk/restful-go/ui/static /static
COPY --from=build /go/src/github.com/oglinuk/restful-go/ui/templates /templates
COPY --from=build /go/src/github.com/oglinuk/restful-go/ui/ui ui
EXPOSE 9042
ENTRYPOINT ["/ui"]
```

This reduces the image size from `948MB` to `6.43MB`.

One thing missed in the code review was a check of the `tpl` variable to
ensure it's not `nil`.

Refactoring `addr` to be comprised of environment variables is done via
`os.Getenv("HOST")` and `os.Getenv("PORT"` in combination with
`fmt.Sprintf`.

Now to refactor all route handler logic from `main.go` to `handlers.go`.

An example (`getBooks`) looks like the following.

```Go
// main.go

r.Get("/" getBooks)// func(w http.ResponseWriter, r *http.Request) {
/*
	br, err := getBooks()
	if err != nil {
		http.Error(w, err.Error(), 500)
	} else {
		err = tpl.ExecuteTemplate(w, "index.html", br)
		if err != nil {
			http.Error(w, err.Error(), 500)
		}
	}
})
*/
```

Time to do the rest ...

The finished result of refactoring all handler logic out of
`cmd/ui/main.go` looks like the following.

```Go
r.Post("/", createBook)
r.Get("/", getBooks)
r.Get("/{id}", getBookById)
r.Get("/ping", getHeartbeat)
r.Get("/create", createBook)
r.Get("/static/*", func(w http.ResponseWriter, r *http.Request) {
	root := http.Dir("static")
	fsrvr := http.StripPrefix("/static/", http.FileServer(root))
	fsrvr.ServeHTTP(w, r)
})
```

All structs in `cmd/ui/models.go` are uppercase (public), which is not
necessary, so changed all to lowercase (private). There were a lot of
places references the uppercase structs, like in `handlers.go`, but this
was easily handled with vi commands like `:%s/BooksResp/booksResp/g`.

`cmd/ui` is missing all test files, so I will start with
`cmd/ui/utils_test.go` since it will be small.

The current size of `handlers.go` is `206` lines, so the better option is
refactoring into separate handler files. The `handlers.go` file has been
split up into `create.go`, `retrieve.go`, and `update.go`. Since we are
using `fetch` with JavaScript to handle the `DELETE` requests, there is
no need for a handler. This may change if `fetch` ends up being the
better option to handle `PUT` requests over a hidden HTML tag. That will
be a decision for the next code review.

I've decided to put off creating tests for the minimal web UI (except for
`utils_test.go`, only because it is not the main focus of this project,
and I need to learn end-to-end testing still. This will be a good
opportunity to learn about `httptest.Server`, as it is "... an HTTP
server listening on a system-chosen port on the local loopback interface,
for use in end-to-end HTTP tests."

The last thing to do for `cmd/ui/main.go` is to refactor `localIP` and
`dockerIP` to use environment variables. In addition, a request to
`dockerIP` is made. If the request fails the `currentIP` is set to
`localIP` values, otherwise it is set to `dockerIP`.

Originally I made a note to change the hardcoded `backend` variable in
`cmd/ui/static/js/index.js`. This I think is actually fine since the
minimal web UI should always be on the same network. Notifying the user
that the request failed is easily done with an `alert` in the `catch`
statement of the fetch call.

Like the hardcoded `backend` variable, I also think that hardcoding the
`<title>RESTful Go</title>` tag in `cmd/ui/templates/header.html` is
fine. This perhaps should be looked at again when the logic for template
execution is refactored into it's own function.

The final thing to do for the `cmd/ui` portion of the 1642914462
code-review is to reference a local `favicon.svg` file in
`cmd/ui/templates/header.html`. I am not familiar with inlining svg's
yet, but referenced a resource below.

Related:

* restful-go
	<https://github.com/oglinuk/restful-go>
* `httptest.Server`
	<https://pkg.go.dev/net/http/httptest#Server>
* Inlining svg
	<https://yoksel.github.io/url-encoder/>

Tags:

	#go #code-sprint #multi-stage #docker #refactoring #test-driven-development
