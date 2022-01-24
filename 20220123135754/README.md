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
.Get("/static/*", func(w http.ResponseWriter, r *http.Request) {
	root := http.Dir("static")
	fsrvr := http.StripPrefix("/static/", http.FileServer(root))
	fsrvr.ServeHTTP(w, r)
})
```

Related:

* restful-go
	<https://github.com/oglinuk/restful-go>

Tags:

	#go #code-sprint #multi-stage #docker #refactoring
