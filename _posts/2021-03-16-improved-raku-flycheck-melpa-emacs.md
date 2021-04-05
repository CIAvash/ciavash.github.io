---
layout: post
title: 'An improved flycheck-raku now available on melpa [Emacs]'
---

Recently I forked the flycheck-raku (by @widefox) to the Raku GitHub organization.
And did some improvements to it and published it on [melpa](https://melpa.org/), so others can easily install and update it.

For those who don't know, [flycheck](https://www.flycheck.org/) is a tool for syntax checking Gnu Emacs buffers.

You can install [flycheck-raku](https://github.com/Raku/flycheck-raku) using [use-package](https://github.com/jwiegley/use-package):

```elisp
(use-package flychek-raku :ensure t)
```

## New features

### Project detection

[![Emacs - flycheck-raku - bare say]({{ site.baseurl }}/uploads/emacs-flycheck-raku-could-not-find-module.png)]({{ site.baseurl }}/uploads/emacs-flycheck-raku-could-not-find-module.png)

Previously if you used `flycheck-raku` on a project, it would show errors on `use SomeModule;`,
even though the module was in the `lib` directory of the project. And this would make `flycheck` kinda
useless, because it wouldn't show further errors.

But in the new version of `flycheck-raku`, project root is detected and its `lib` directory is added to
include path. So no more errors on valid modules.


### Error pattern improvements

#### Full error messages

Previous versions of `flycheck-raku` would cut some long error messages. Now, error messages are fully shown.

#### Multi-line error messages

![Emacs - flycheck-raku - bare say]({{ site.baseurl }}/uploads/emacs-flycheck-raku-bare-say.png)

In the new version, multi-line error messages are fully shown.

#### Potential difficulties

![Emacs - flycheck-raku - symbol redclaration]({{ site.baseurl }}/uploads/emacs-flycheck-raku-symbol-redclaration.png)

New version shows potential difficulties; I've only seen one such error message and that is `Redclaration of symbol $x`.