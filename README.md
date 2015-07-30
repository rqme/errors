errors
======

Go wrapper for multiple errors


## Getting Started

### Installing

To start using errors, install Go and run `go get`:

```sh
$ go get github.com/rqme/errors
```

### Using

Using **errors** is as simple as 

```go
import . "github.com/rqme/errors"
...
func main() {
	
	errs := new(Errors)
	...
	if err := os.Create("foo.txt"); err != nil {
		errs.Add(err)
	}
	...
	err := fmt.Errorf("Something didn't work, %s", "Jack")
	errs.Add(Err)
	...
	log.Fatal(errs.Err())
}
```
The **errors** package name conflicts with the standard package errors so you can use the **.** prefix to hide it.

Note: errors is not concurrency safe. This can be done with the sync package

```go
import (
	. "github.com/rqme/errors"
	"sync"
)
...
func main() {
	errs = new(Errors)
	m := new(sync.Mutex)
	addErr := func(err error) {
		m.Lock()
		errs.Add(err)
		m.Unlock()
	}
	...
	go func() {
		err := ...
		addErr(Err)
	}
	...
	log.Fatal(errs.Err())
}
...