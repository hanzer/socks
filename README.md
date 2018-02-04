SOCKS
=====

SOCKS is a SOCKS4, SOCKS4A and SOCKS5 proxy package for Go.

## Quick Start
### Get the package

    go get -v github.com/hanzer/socks

### Import the package

    import "github.com/hanzer/socks"

### Create a SOCKS proxy dialing function

    dialSocksProxy := socks.DialSocksProxy(socks.SOCKS5, "127.0.0.1:1080")
    tr := &http.Transport{Dial: dialSocksProxy}
    httpClient := &http.Client{Transport: tr}

## Example

```go
package main

import (
	"fmt"
	"io/ioutil"
	"log"
	"net/http"

	"h12.me/socks"
)

func main() {
	dialSocksProxy := socks.DialSocksProxy(socks.SOCKS5, "127.0.0.1:9050")
	tr := &http.Transport{Dial: dialSocksProxy}
	httpClient := &http.Client{Transport: tr}
	resp, err := httpClient.Get("http://www.google.com")
	if err != nil {
		log.Fatal(err)
	}
	defer resp.Body.Close()
	if resp.StatusCode != http.StatusOK {
		log.Fatal(resp.StatusCode)
	}
	buf, err := ioutil.ReadAll(resp.Body)
	if err != nil {
		log.Fatal(err)
	}
	fmt.Println(string(buf))
}
```

## Alternatives
http://godoc.org/golang.org/x/net/proxy
