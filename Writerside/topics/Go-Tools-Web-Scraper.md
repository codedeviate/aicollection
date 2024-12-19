# Web Scraper

To create a web scraper program in Go, follow these steps:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir webscraper
cd webscraper
go mod init github.com/username/webscraper
```

## Step 2: Install Dependencies

You will need the `goquery` library for parsing HTML.

```sh
go get github.com/PuerkitoBio/goquery
```

## Step 3: Create the `scraper.go` File

Create a `scraper.go` file to handle the web scraping functionality.

```go
// scraper.go
package main

import (
    "fmt"
    "log"
    "net/http"
    "github.com/PuerkitoBio/goquery"
)

// Scrape fetches the HTML content of a URL and prints the text of the specified elements.
func Scrape(url string, selector string) {
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

    doc.Find(selector).Each(func(index int, item *goquery.Selection) {
        text := item.Text()
        fmt.Println(text)
    })
}
```

## Step 4: Create the `main.go` File

Create a `main.go` file to start the web scraper.

```go
// main.go
package main

import (
    "fmt"
    "os"
)

func main() {
    if len(os.Args) != 3 {
        fmt.Println("Usage: webscraper <url> <selector>")
        os.Exit(1)
    }

    url := os.Args[1]
    selector := os.Args[2]
    fmt.Printf("Scraping URL: %s with selector: %s\n", url, selector)
    Scrape(url, selector)
}
```

## Step 5: Run the Program

Run the program using the `go run` command.

```sh
go run main.go <url> <selector>
```

Replace `<url>` with the URL you want to scrape and `<selector>` with the CSS selector of the elements you want to extract. This will start the web scraper and print the text of the specified elements found on the specified URL.