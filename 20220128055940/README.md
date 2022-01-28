# Why `localhost` (`127.0.0.1`) is so Powerful

~16.7 million reserved IP addresses that every device has.

Localhost is `127.0.0.0/8`, which means the number of usable hosts is
`16,777,214`. Each IP address has 65535 ports (less in practice since
some ports are reserved, and other used for common applications). This
means that a web server running on `127.0.0.1:9001` does not conflict
with a web server running on `127.0.0.2:9001`, or `127.0.1.1:9001`, or
`127.1.1.1:9001`, and so on.

I encourage you to test out what I said about with the simple web server
Go snippet below.

```Go
package main

import (
	"log"
	"net/http"
)

func main() {
	http.HandlerFunc("/", func(w http.ResponseWriter, r *http.Request) {
		fmt.Fprintf(w, "hello, world!")
	})

	// Change `127.0.0.1` to `127.0.1.1` in a copy and run it as well
	log.Fatal(http.ListenAndServe("127.0.0.1:9001", nil))
}
```

Related:

* RFC 6761 (section 6.3)
	<https://datatracker.ietf.org/doc/html/rfc6761#section-6.3>
* RFC 5735 (section 4)
	<https://datatracker.ietf.org/doc/html/rfc5735#section-4>
* RFC 2606 (section 2)
	<https://datatracker.ietf.org/doc/html/rfc2606#section-2>
	Subnet calculator (very bottom has a table of subnets)
* <https://www.calculator.net/ip-subnet-calculator.html>

Tags:

	#localhost #networking #go
