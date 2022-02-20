# Exploring the `locallimit`

For a while I have known about the *power of `localhost`*, but have never
really tested the real limits of it. To put it's power to the test, I've
started a project called *locallimit*. The first go at the program is as
follows.

```Go
package main

import (
	"flag"
	"fmt"
	"io"
	"log"
	"net/http"
	"os"
	"runtime"
	"sync"
	"syscall"
)

var (
	firstBound = flag.Int("fb", 256, "First octet limit (max 256)")
	secondBound = flag.Int("sb", 100, "Second octet limit (max 256)")
	thirdBound = flag.Int("tb", 10, "Third octet limit (max 256)")
)

func newHandler(addr string) http.HandlerFunc {
	return func(w http.ResponseWriter, r *http.Request) {
		fmt.Fprintf(w, addr)
	}
}

func newServer(addr string, handler http.Handler) *http.Server {
	return &http.Server{
		Addr: addr,
		Handler: handler,
	}
}

func init() {
	if runtime.GOOS != "windows" {
		var rLimit syscall.Rlimit
		syscall.Getrlimit(syscall.RLIMIT_NOFILE, &rLimit)
		rLimit.Cur = rLimit.Max
		syscall.Setrlimit(syscall.RLIMIT_NOFILE, &rLimit)
	}

	flag.Parse()
}

func main() {
	f, err := os.Create("localhost.log")
	if err != nil {
		log.Fatal(err.Error())
	}
	defer f.Close()

	mr := io.MultiWriter(os.Stdout, f)

	log.SetOutput(mr)

	wg := &sync.WaitGroup{}
	basePort := 9001

	for i := 1; i < *thirdBound; i++ {
		for j := 0; j < *secondBound; j++ {
			for k := 0; k < *firstBound; k ++ {
				addr := fmt.Sprintf("127.%d.%d.%d:%d", k, j, i, basePort+(i+j+k))

				wg.Add(1)
				go func(addr string) {
					s := newServer(addr, newHandler(addr))
					go log.Fatal(s.ListenAndServe())
					wg.Done()
				}(addr)

				log.Printf("Serving at %s ...\n", addr)
			}
		}
	}
	wg.Wait()
	for{}
}
```

My laptop with 8GB of RAM can only reach about 697000 web servers before
running out of memory, which is only a scratch of the ~16.5 million
available addresses.

More to come.

Tags:

	#go #localhost #limits
