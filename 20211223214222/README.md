# Learning Lab: Create Simple TCP/IP Server in Go

This lab focuses on the `net` package of the standard library. The first
thing to do is to allow for the `PORT` variable to be configurable, which
is done using `os.Getenv`. It's always good to add a check and a default,
which looks like the following.

```Go

PORT := os.Getenv("PORT")
if PORT == "" {
	PORT = "9001"
}
```

Since `os.Getenv` returns a `string`, we check if `PORT` is an empty
string rather than if its `nil`.

The next task is to print a greeting on a new inbound connection. This is
where `net` comes in. The example for a simple tcp server in the
documentation is the following.

```Go
ln, err := net.Listen("tcp", ":8080")
if err != nil {
	// handle error
}
for {
	conn, err := ln.Accept()
	if err != nil {
		// handle error
	}
	go handleConnection(conn)
}
```

My implementation looks like the following.

```Go
addr := fmt.Sprintf("0.0.0.0:%s", PORT)

lis, err := net.Listen("tcp", addr)
if err != nil {
	log.Fatal(err)
}

log.Printf("Server is running at %s ...", addr)
for {
	conn, err := lis.Accept()
	if err != nil {
		log.Fatal(err)
	}

	welcome := fmt.Sprintf("Hello %s!\n", conn.RemoteAddr().String())
	conn.Write([]byte(welcome))
}
```

I added a print statement to log that the server is running and what
address its listening on. I also added `conn.RemoteAddr().String()` to
the greeting, which returns the remote network address.

The last task is to enable a minimal set of commands. Unfortunately the
example implementations of `net.Listener` in the documentation don't
really cover how to handle input from `net.Conn`. After taking a look at
the example solution, it uses `bufio.NewScanner` and loops over the
scanned lines using a `switch` statement. I like this approach rather
than approaches I found online that use a `for` loop and reading the
input into a buffer.

My implementation is going to use `bufio.NewReader` instead of scanner,
and looks like the following.

```Go
func handle(c net.Conn) {
	defer c.Close()

	br := bufio.NewReader(c)

	remoteAddr := c.RemoteAddr().String()

	for {
		fmt.Fprintf(c, "> ")

		line, err := br.ReadString('\n')
		if err != nil {
			if err == io.EOF {
				continue
			}
			log.Println(err)
		}

		line = strings.TrimeSpace(line)
		log.Printf("%s > %s\n", remoteAddr, line)

		switch line {
			case "ip":
				fmt.Fprintf(c, "%s\n", remoteAddr)
			case "rng":
				fmt.Fprintf(c, "%d\n", rand.Int63())
			case "time":
				fmt.Fprintf(c, "%s\n", time.Now())
			default:
				fmt.Fprintf(c, "commands: ip|rng|time\n")
		}
	}
}
```

One thing to mention is rather than having to call `c.Write` and pass
`[]byte` everytime, or write a helper function, I chose to use
`fmt.Fprintf`. It's like `fmt.Printf`, but allows you to pass an
`io.Writer` (`net.Conn` in this case).

When building/running the server and connecting to it using `nc localhost
9001`, I got the following results.

```BASH
Hello 127.0.0.1:48202!
>
commands: ip|rng|time
> ip
127.0.0.1:48202
> rng
5577006791947779410
> time
2021-12-23 15:28:39.715435996 -0800 PST m=+13.929682867
```

There are two extra tasks, which are to create a `Dockerfile` and a
`docker-compose.yaml` file. Since I love both, I will quickly implement
them.

The `Dockerfile` looks like the following.

```Dockerfile
FROM go:1.17
ADD . /tcp-server
WORKDIR /tcp-server
RUN go build -o tcp-server
EXPOSE 9001
CMD ["./tcp-server"]
```

The `docker-compose.yaml` file looks like the following.

```
version: "3.9"
services:
  server:
    build: .
    ports:
      - "9001:9001"
    environment:
      - PORT=9001
```

Related:

* <https://github.com/rwxrob/lab-go-tcp-server>
* <https://pkg.go.dev/net>
* <https://pkg.go.dev/net#example-Listener>
* <https://pkg.go.dev/bufio>
* <https://pkg.go.dev/bufio#Reader.ReadString>
* <https://pkg.go.dev/fmt#Fprintf>
* <https://docs.docker.com/engine/reference/builder/>
* <https://docs.docker.com/compose/compose-file/compose-file-v3/>
* <https://github.com/oglinuk/simple-tcp-server>

Tags:

	#go #net #tcp #ocms #lab
