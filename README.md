[![GoDoc](https://godoc.org/github.com/Joker/jade?status.svg)](https://godoc.org/github.com/Joker/jade)

# Jade.go - template engine for Go (golang)
Package jade (github.com/Joker/jade) implements Jade-lang templates for generating Go html/template output.

## Jade syntax
example:
```jade
doctype html
html(lang="en")
  head
    title= pageTitle
    script(type='text/javascript').
      if (foo) {
         bar(1 + 5)
      }
  body
    h1 Jade - template engine
    #container.col
      if youAreUsingJade
        p You are amazing
      else
        p Get on it!
      p.
        Jade is #[a(terse)] and simple
        templating language with a
        #[strong focus] on performance
        and powerful features.
```
becomes
```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <title>{{ pageTitle }}</title>
        <script type='text/javascript'>
            if (foo) {
                bar(1 + 5)
            }
        </script>
    </head>
    <body>
        <h1>Jade - template engine</h1>
        <div id="container" class="col">
            {{ if youAreUsingJade }}
                <p>You are amazing</p>
            {{ else }}
                <p>Get on it!</p>
            {{ end }}
            <p>
                Jade is <a terse="terse"></a> and simple
                templating language with a
                <strong>focus</strong> on performance
                and powerful features.
            </p>
        </div>
    </body>
</html>
```

### Example usage

```go
package main

import (
    "fmt"
    "github.com/Joker/jade"
)

func main() {
    tpl, err := jade.Parse("name_of_tpl", "doctype 5: html: body: p Hello world!")
    if err != nil {
        fmt.Printf("Parse error: %v", err)
        return
    }

    fmt.Printf( "Output:\n\n%s", tpl  )
}
```

Output:

```html
<!DOCTYPE html>
<html>
    <body>
        <p>Hello world!</p>
    </body>
</html>
```
