---
layout: post
title: How to type Raku unicode characters in Emacs
---

[Raku programming language](https://raku.org/) uses some unicode characters as operators, quotation marks, etc.
In this post I'm going to explain how to type those characters in Emacs using
[input methods](http://www.emacswiki.org/emacs/InputMethods).

First, you might want to see a list of those characters and their ASCII equivalents
[here](https://docs.raku.org/language/unicode_ascii).
There is also a doc for [entering unicode characters](https://docs.raku.org/language/unicode_entry).
You may specifically want to look at [XCompose](https://en.wikipedia.org/wiki/Compose_key#GNU.2FLinux) for a system-wide solution.

There are at least two input methods you can use to enter the unicode characters used in Raku.
[rfc1345](https://tools.ietf.org/html/rfc1345) and [TeX](http://www.emacswiki.org/emacs/TeXInputMethod).

To select an input method type `C-x RET C-\` and to switch to an input method use `C-u C-\`.
`C-\` can be used to toggle input method.

After you select an input method, You have to use the prefix character it provides for typing special characters.
`&` is the prefix used for rfc1345 and `\`, `^` and some other characters are used for TeX.

Example for typing λ:

rfc1345: `&l*`

TeX: `\lambda`

To see a list of character sequences for an input method, type `C-h I`.

You can change the default input method by setting the `default-input-method` variable:

{% highlight elisp %}
(setq default-input-method 'TeX)
{% endhighlight %}

To add characters which are not available in an input method:

{% highlight elisp %}
(eval-after-load "quail/latin-ltx"
  `(let ((quail-current-package (assoc "TeX" quail-package-alist)))
     (quail-define-rules ((append . t))
                         ("\\lcb" ?｢)
                         ("\\rcb" ?｣))))
{% endhighlight %}

Now with TeX method enabled, `\lcb` types '｢' and `\rcb` types '｣'.

Same thing for the rfc1345 input method:

{% highlight elisp %}
(eval-after-load "quail/rfc1345"
  `(let ((quail-current-package (assoc "rfc1345" quail-package-alist)))
    (quail-define-rules ((append . t))
                        ("&[" "｢")
                        ("&]" "｣"))))
{% endhighlight %}

Now with the rfc1345 method you can type '｢' with `&[` and type '｣' with `&]`.

Another way of entering unicode characters is using `C-x 8 RET` which runs `insert-char` command.
`C-x 8` prefix key has shortcuts for some characters. For example, `C-x 8 / /` inserts ÷. To add your own characters:

{% highlight elisp %}
(global-set-key (kbd "C-x 8 l") "λ")
{% endhighlight %}
or:
{% highlight elisp %}
(global-set-key (kbd "C-x 8 l") (lambda () (interactive) (insert "λ")))
{% endhighlight %}

Now `C-x 8 l` inserts λ.

Below is a list of unicode characters used in Raku and their character sequences in rfc1345 and TeX.

**Note**: rfc1345 character mnemonics work in Vim too. You only need to replace `&` with `Ctrl-K`.

| Character | C-x 8         | rfc1345       | TeX          |
|:---------:|:-------------:|:-------------:|:------------:|
| «         | `<`           | `&<<`         | `\flqq`      |
| »         | `>`           | `&>>`         | `\frqq`      |
| ×         | `x`           | `&*X`         | `\times`     |
| ÷         | `/ /`         | `&-:`         | `\div`       |
| −         | `_ -`         | `&-2`         | `\minus`     |
| ≤         | `_ <`         | `&=<`         | `\le`        |
| ≥         | `_ >`         | `&>=`         | `\ge`        |
| ≠         | `/ =`         | `&!=`         | `\ne`        |
| ∘         |               | `&Ob`         | `\circ`      |
| ≅         |               | `&?=`         | `\cong`      |
| π         |               | `&p*`         | `\pi`        |
| τ         |               | `&t*`         | `\tau`       |
| ∞         |               | `&00`         | `\infty`     |
| …         |               | `&.3`         | `\ldots`     |
| ‘         | `[`           | `&'6`         | `\rq`        |
| ’         | `]`           | `&'9`         | `\lq`        |
| ‚         |               | `&.9`         | `\glq`       |
| “         | `{`           | `&"6`         | `\ldq`       |
| ”         | `}`           | `&"9`         | `\rdq`       |
| „         |               | `&:9`         | `\glqq`      |
| ¯         | `=`           | `&'m`         | `\={}`       |
| ⁻         |               | `&-S`         | `^-`         |
| ⁺         |               | `&+S`         | `^+`         |
| ⁰ - ⁹     | `^ 1` - `^ 3` | `&0S` - `&9S` | `^0` - `^9`  |
| ½         | `1 / 2`       | `&12`         | `\frac12`    |
| ∅         |               | `&/0`         | `\emptyset`  |
| ∈         |               | `&(-`         | `\in`        |
| ∉         |               |               | `\notin`     |
| ∋         |               | `&-)`         | `\ni`        |
| ⊆         |               | `&(_`         | `\subseteq`  |
| ⊈         |               |               | `\nsubseteq` |
| ⊂         |               | `&(C`         | `\subset`    |
| ⊄         |               |               | `\nsubset`   |
| ⊇         |               | `&)_`         | `\supseteq`  |
| ⊉         |               |               | `\nsupseteq` |
| ⊃         |               | `&(C`         | `\supset`    |
| ⊅         |               |               | `\nsupset`   |
| ∪         |               | `&)U`         | `\cup`       |
| ∩         |               | `&(U`         | `\cap`       |
| ∖         |               |               | `\setminus`  |
| ⊖         |               |               | `\ominus`    |
| ⊎         |               |               | `\uplus`     |
| ≡         |               | `&=3`         | `\equiv`     |
| ≢         |               |               | `\nequiv`    |
{: .table style="font-family: sans-serif;"}