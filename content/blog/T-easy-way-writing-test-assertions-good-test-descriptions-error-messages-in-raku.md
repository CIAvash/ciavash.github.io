---
title: T - Easy way of writing test assertions which output good test descriptions and error messages in Raku
date: 2022-02-13
categories: [Raku, Programming, Raku Module, Testing]
tags: [Raku, Testing, Module, Rakue Module, Slang, Assertion]
---

After I finished watching [Daniel Sockwell](https://www.codesections.com/)'s [FOSDEM 2022 Raku
presentation](https://fosdem.org/2022/schedule/event/simpletesting/), I thought this is a good opportunity to play with
[Raku](https://www.raku-lang.ir/en)'s [slangs](https://design.raku.org/S99.html#slang), something I hadn't done before.

What is Daniel's talk(and upcoming module) and my module going to solve?
- Write less but more readable test code
- Get a useful test description and failure message

If you use [`cmp-ok`](https://docs.raku.org/type/Test#sub_cmp-ok), you get a good error message; but without a test
description it's sometimes hard to understand.  Also `cmp-ok` and other test functions(most of them, `use-ok` being an
exception for example) do not output anything on a successful test, unless you provide the description yourself.  I
personally think that test sub routines should generate a description if one is not provided.  But of course that
cannot be done with simple functions. Maybe the [Test](https://docs.raku.org/type/Test) module needs to be rethought in the future?

So I made the [T](https://github.com/CIAvash/T) slang which provides the `t` keyword for writing test assertions.  I didn't
want to make it complicated, so it's a very short and simple slang which takes an expression of form `<got> <infix>
<expected>`.

The current status of the module: It works for me!

Here are some examples:

```raku
use T:auth<zef:CIAash>;

t 4 == 4;
=output ok 1 - 4 == 4

t $my_great_module.return('something') eq 'something';
=output ok 2 - $my_great_module.return('something') eq 'something'

t $my_great_module.return('something else') eq 'something';
=output not ok 3 - $my_great_module.return('something else') eq 'something'
# Failed test '$my_great_module.return('something else') eq 'something''
# at ... line ...
# expected: "something"
#  matcher: 'infix:<eq>'
#      got: "something else"
```
