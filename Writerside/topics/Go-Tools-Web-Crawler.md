# Web Crawler

To create a web crawler program in Go, follow these steps:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir webcrawler
cd webcrawler
go mod init github.com/username/webcrawler
```

## Step 2: Install Dependencies

You will need the `goquery` library for parsing HTML.

```sh
go get github.com/PuerkitoBio/goquery
```

## Step 3: Create the `crawler.go` File

Create a `crawler.go` file to handle the web crawling functionality.

```go
// crawler.go
package main

import (
    "fmt"
    "log"
    "net/http"
    "github.com/PuerkitoBio/goquery"
)

// Crawl fetches the HTML content of a URL and prints the links found.
func Crawl(url string) {
    resp, err := http.Get(url)
    if err != nil {
        log.Fatalf("Failed to fetch URL: %v", err)
    }
    defer resp.Body.Close()

    if resp.StatusCode != 200 {
        log.Fatalf("Failed to fetch URL: %s", resp.Status)
    }

    doc, err := goquery.NewDocumentFromReader(resp.Body)
    if err != nil {
        log.Fatalf("Failed to parse HTML: %v", err)
    }

    doc.Find("a").Each(func(index int, item *goquery.Selection) {
        link, _ := item.Attr("href")
        fmt.Println(link)
    })
}
```

## Step 4: Create the `main.go` File

Create a `main.go` file to start the web crawler.

```go
// main.go
package main

import (
    "fmt"
    "os"
)

func main() {
    if len(os.Args) != 2 {
        fmt.Println("Usage: webcrawler <url>")
        os.Exit(1)
    }

    url := os.Args[1]
    fmt.Printf("Crawling URL: %s\n", url)
    Crawl(url)
}
```

## Step 5: Run the Program

Run the program using the `go run` command.

```sh
go run main.go <url>
```

Replace `<url>` with the URL you want to crawl. This will start the web crawler and print the links found on the specified URL.