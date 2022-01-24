# Don't Downplay Progress

I feel so stupid. Something like interfaces are so crucial to understand,
especially when using a programming language like Golang. In Golang,
"interfaces are implemented implicitly". Today this really clicked for
me, and I hope to make it click for you as well.

To give context, I am writing a test to ensure my function handles an
`io.ReadCloser` input that is not `nil`, but will cause `json.Decode` to
fail.

My first thought was to use `bytes.NewBufferString(`"{'test': 'bad}"`)`,
but got the following error when trying to assign to
`http.Response.Body`.

```
./utils_test.go:30:14: cannot use bytes.NewBufferString("{\"test\":\"bad}") (type *bytes.Buffer) as type io.ReadCloser in assignment:
        *bytes.Buffer does not implement io.ReadCloser (missing Close method)
FAIL    github.com/oglinuk/restful-go/cmd/ui [build failed]
```

The key that I've always glossed over in the above output is `(missing
Close method)`.

If we look at the interface type section of the Golang specification, it
states "An interface type specifies a method set called its interface."
If we look at the method sets section, it states "A type has a (possibly
empty) method set associated with it. The method set of an interface type
is its interface. The method set of any other type T consists of all
methods declared with receiver type T."

The key sentence is "The method set of any other T consists of all
methods declard with receiver type T". In our context, the receiver type
is `ReadCloser`, and the method set is "the basic Read and Close
methods." The `bytes.Buffer` struct implements the `Read` method, but not
the `Close` method.

When going to `io.ReadCloser`, I came across `io.NopCloser`, which "
returns a ReadCloser with a no-op Close method wrapping the provided
Reader r."

I encourage you to write your own test for the following code.

```Go
package main

import (
        "encoding/json"
        "fmt"
        "io"
)

func decodeJSON(v interface{}, body io.ReadCloser) error {
        if v == nil {
                return fmt.Errorf("decodeJSON::v is nil")
        }

        if body == nil {
                return fmt.Errorf("decodeJSON::body is nil")
        }
        defer body.Close()

        err := json.NewDecoder(body).Decode(&v)
        if err != nil {
                return err
        }

        return nil
}
```

Don't downplay progress, cause you never know when reality will hit you
in the face.

Related:

* Golang interfaces
	<https://go.dev/ref/spec#Interface_types>
* Golang method sets
	<https://go.dev/ref/spec#Method_sets>
* "interfaces are implemented implicity"
	<https://go.dev/tour/methods/10>

Tags:

	#imposter-syndrome #click-moment #go-interfaces #go-method-sets #go-testing
