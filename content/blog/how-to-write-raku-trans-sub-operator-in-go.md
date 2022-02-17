---
title: How to write Raku's trans routine/operator in Go
date: 2022-02-13
categories: [Raku, Go, Programming]
tags: [Raku, Go, Golang, Translate, Transliteration, Web Scraping, CSS Selectors]
---

I was looking for a way to transliterate(translate) English numbers to Persian numbers in Go. 
Such functionality is usually found in programming languages, but I wasn't expecting too much from Go.

It's very easy to do in [Raku](https://www.raku-lang.ir/en):
```raku
say 567.trans: '0'..'9' => '۰'..'۹'
=output ۵۶۷␤

say TR/0..9/۰..۹/ given 567
=output ۵۶۷␤
```

For Go I found [xstrings](https://pkg.go.dev/github.com/huandu/xstrings) module which has a
[`Translate`](https://pkg.go.dev/github.com/huandu/xstrings#Translate) function.  But the solution I came up with was using
[`NewReplacer`](https://pkg.go.dev/strings#Replacer) function from Go's internal [strings](https://pkg.go.dev/strings)
module:
```go
package main

import (
	"fmt"
	"strings"
)

func main() {
	fmt.Println(strings.NewReplacer(`0`, `۰`, `1`, `۱`, `2`, `۲`, `3`, `۳`, `4`, `۴`, `5`, `۵`, `6`, `۶`, `7`, `۷`, `8`, `۸`, `9`, `۹`).Replace(`567`))
}
```
[Go playground link](https://go.dev/play/p/-o0OUvoLKsm)

This could be easier to write if Go had a `zip` function, so you could zip two slices (or ranges if Go had a range
operator) and then use the `...` unpack operator. Or `Replacer` could have a method that took two slices or better two
ranges(that is, if Go had it), specially now that Generics are coming to Go.

Unrelated to the title of this blog post, I was also looking for a module to parse HTML documents using CSS selectors;
my search led me to [goquery](https://pkg.go.dev/github.com/PuerkitoBio/goquery). Which was what I wanted, but I
couldn't find an easy way to get the whitespace-trimmed text content of HTML elements; there was a `Text` function, but
that contained everything. It seems it's not just the way of thinking of the Go language that makes me want more, but
also some Go modules. So I ended up writing a recursive function to trim whitespace using `strings.TrimSpace` and join texts.

This is how I would do it in Raku, using [DOM::Tiny](https://github.com/zostay/raku-DOM-Tiny) (also containing the previous code):
```raku
put $dom.find('.my-element > div').map(*.all-text(:trim)).join("\n").trans: '0'..'9' => '۰'..'۹';
```

And this is my Go solution(maybe there are better ways to do it, that I'm not aware of, or even better way to write my code):
```go
// ........
	text := strings.Join(doc.Find(`.my-element > div`).Map(getText), "\n")

	text = strings.NewReplacer(`0`, `۰`, `1`, `۱`, `2`, `۲`, `3`, `۳`, `4`, `۴`, `5`, `۵`, `6`, `۶`, `7`, `۷`, `8`, `۸`, `9`, `۹`).Replace(text)

	fmt.Println(text)
// ........

func getText (_ int, s *goquery.Selection) string {
	if children := s.ChildrenFiltered(`:not(img)`); children.Text() != `` {
		return strings.Join(children.Map(getText), ` `)
	} else {
		return strings.TrimSpace(s.Text())
	}
}
```

Another solution is using the `regexp` module to replace all whitespace:
```go
// ........
	text := strings.Join(doc.Find(`.my-element > div`).Map(func(_ int, s *goquery.Selection) string {
		re := regexp.MustCompile(`\s+`)
		return re.ReplaceAllLiteralString(s.Text(), ` `)
	}), "\n")

	text = strings.NewReplacer(`0`, `۰`, `1`, `۱`, `2`, `۲`, `3`, `۳`, `4`, `۴`, `5`, `۵`, `6`, `۶`, `7`, `۷`, `8`, `۸`, `9`, `۹`).Replace(text)

	fmt.Println(text)
// ........
```

What I get from Go is speed, so I won't complain too much 😀

And just for fun, I'm still seeing this when I visit https://pkg.go.dev :
![pkg.go.dev blocked for Iran by Google](/img/pkg.go.dev-blocked-for-Iran-by-Google.png)
