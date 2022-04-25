---
title: "flymake-rakudo - Another syntax checker for Raku on Emacs"
date: 2022-04-25
categories: [Raku, Rakudo, Emacs, Tools]
tags: [Raku, Rakudo, Emacs, Flymake, Syntax Checking]
---

# Flymake

I've been switching to [Emacs](https://www.gnu.org/software/emacs/) packages which are lighter and use the internal Emacs system,
instead of creating their own. This time I wanted to try
[Flymake](https://www.gnu.org/software/emacs/manual/html_node/flymake/index.html), the syntax checker that comes with Emacs. At
first it wasn't very appealing because I thought it would only show the error on mouse hover! So I tried to see what options I
have for displaying the error messages when text cursor moves over them.

# Eldoc

The first step was using and tweaking [Eldoc](http://elpa.gnu.org/packages/eldoc.html). Flymake shows errors by adding
`flymake-eldoc-function` to `eldoc-documentation-functions` list. But by default Eldoc only shows one message at a time and the
priority is with the order of the documentation functions.

Fortunately there is a customization option for showing messages. The name of this option is `eldoc-documentation-strategy`, you
can see its values and change it using `customize-group` or `customize-option` commands. The value I was interested in was
`eldoc-documentation-compose`; this function waits for all strings and then shows them. But changing this option is not enough if
there are more than one messages, you have to change the `eldoc-echo-area-use-multiline-p` option as well; I set it to `always`.

## Eglot

A word of caution! If you use [Eglot](https://github.com/joaotavora/eglot)(An LSP client), then make sure to add
`eldoc-documentation-strategy` to its `eglot-stay-out-of` list. 'Cause Eglot sets it to `eldoc-documentation-enthusiast` which
caused a lot of head scratching.

```elisp
(add-to-list 'eglot-stay-out-of 'eldoc-documentation-strategy)
```

## Eldoc-box

Now Eldoc can show all messages, documentation and Flymake diagnostics. But it shows them in the echo area. So I looked for a
package to show it as a child frame. The package I found was [eldoc-box](https://github.com/casouri/eldoc-box).

# Flymake-rakudo

![flymake-rakudo screenshot](/img/flymake-rakudo-screenshot.png)

Now that I could see Flymake as a viable option, I had to create a syntax checker for [Raku](https://www.raku-lang.ir/en/) using
the [Rakudo](https://rakudo.org/) implementation, because that is the language I use most. Of course there is a
[flymake-flycheck](https://github.com/purcell/flymake-flycheck) package for using Flycheck checkers as Flymake backends and I
could use it with [flycheck-raku](https://github.com/Raku/flycheck-raku), but I decided to create one for Flymake. With a great
timing, recently a package was released for Emacs which makes it easier to create Flymake checkers.

## Flymake-collection

That package is [flymake-collection](https://github.com/mohkale/flymake-collection), it provides a collection of Flymake checkers
and helpers for creating checkers. At first I tried to use the regex from `flycheck-raku`, but then I saw that
`flymake-collection` had `flymake-collection-define-enumerate` and `flymake-collection-parse-json` functions for creating a
checker using JSON output. So I decided to set the `RAKU_EXCEPTIONS_HANDLER` environment variable to `JSON` and parse the output
of that.

It wasn't an easy job at all, because I don't really know Emacs Lisp! And to create a flexible diagnostics generator, I had to
work with Elisp's data structures. So I had no idea what I was doing! After playing with it for a while, reading the documentation
and a lot of struggling, I learned a bit about association lists and managed to use them.

I also had to do a bit more because of how Rakudo outputs the errors; e.g. Parsing a JSON field separately, finding the error column
from its position. But I finally did it and I'm happy with it so far. Of course it needs to be used more to find bugs or other
special cases.

So there you have it: [flymake-rakudo](https://github.com/Raku/flymake-rakudo).

# Final words

Even with all that, I hope we'll see a language server implementation for Raku.
