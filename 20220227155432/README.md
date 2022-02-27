# How to Access Private Fields in Go Structs

When changing my Go labs to a TDD approach, I came into an obstacle when
it came to creating a `sync.WaitGroup`. Part of my approach has been to
write tests against the standard library APIs themselves, so I wanted to
test each method. The `Add` method seemed the easiest as it is
essentially just checking the counter after adding to it. The problem is
the `WaitGroup` count field is private (unexported) and does not expose
any way of accessing it.

The field we are after is `state1`, which looks like the following.

```Go
// 64-bit value: high 32 bits are counter, low 32 bits are waiter
// count.
// 64-bit atomic operations require 64-bit alignment, but 32-bit
// compilers do not ensure it. So we allocate 12 bytes and then use
// the aligned 8 bytes in them as state, and the other 4 as storage
// for the sema.
state1 [3]uint32
```

After a quick search I came across the suggestion of using package
`reflect`. The logic to grab `state1` looks like the following.

```Go
package main

import (
	"fmt"
	"reflect"
	"sync"
)

func main() {
	wg := &sync.WaitGroup{}
	wg.Add(42)

	wgv := reflect.ValueOf(wg).Elem()
	state1 := wgv.FieldByName("state1")
	count := state1.Index(1).Uint()

	fmt.Println(count)
}
```

Related:

	* Go Labs
	<https://github.com/oglinuk/labs/tree/master/go>
	* `sync.WaitGroup` (go 1.17)
	<https://cs.opensource.google/go/go/+/go1.17.7:src/sync/waitgroup.go;l=20>
	* Package `reflect`
	<https://pkg.go.dev/reflect>
