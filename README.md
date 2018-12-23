# Heroku Platform API

[![GoDoc](https://godoc.org/github.com/heroku/heroku-go/v4?status.svg)](https://godoc.org/github.com/heroku/heroku-go/v4)

An API client interface for Heroku Platform API for the Go (golang)
programming language.

## Installation

Going updates will only be made to to `github.com/heroku/heroku-go/v4`, which
supports Go 1.11 modules.

To use this package with Go 1.11 module support simply run `go build` in your
project (with `GO111MODULE=on`.)

To use this package without Go 1.11 module support [TODO] 

It is **not** recommended to use the older `github.com/heroku/heroku-go/v3`
package. This package only exists to prevent breaking existing dependencies
that require it.

## Example

```go
package main

import (
	"context"
	"flag"
	"fmt"
	"log"

	"github.com/heroku/heroku-go/v4"
)

var (
	username = flag.String("username", "", "api username")
	password = flag.String("password", "", "api password")
)

func main() {
	log.SetFlags(0)
	flag.Parse()

	heroku.DefaultTransport.Username = *username
	heroku.DefaultTransport.Password = *password

	h := heroku.NewService(heroku.DefaultClient)
	addons, err := h.AddOnList(context.TODO(), &heroku.ListRange{Field: "name"})
	if err != nil {
		log.Fatal(err)
	}
	for _, addon := range addons {
		fmt.Println(addon.Name)
	}
}
```
