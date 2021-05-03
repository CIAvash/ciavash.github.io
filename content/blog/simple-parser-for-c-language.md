---
date: "2013-07-02T00:00:00Z"
title: Simple parser for C language
tags: [Perl, C, Programming Language, Parser]
aliases:
    - /blog/2013/07/02/simple-parser-for-c-language.html
---

For a long time I'v wanted to push my Parser project which was a university project for Principles of Compiler Design course to GitHub. Now I’v found the time to do it and you can download it [here](https://github.com/CIAvash/simple-c-parser/).

2 years ago I started learning Perl, soon Perl became my favourite programming language. It was then that our professor gave us the scanner project for C language. He told us that we can use the programming language of our choice. We were also allowed to use regular expressions. So I thought Perl is the best language for writing the project. In a month I read [Learning Perl](http://en.wikipedia.org/wiki/Learning_Perl) book and other necessary stuff and became ready to write the scanner. Scanner was my first Perl project. When I gave the project to professor, he said that I was the first person who has written the project in Perl :)

After Scanner, professor gave us a simple C grammar for a parser project. I wrote that in Perl too. The result (with a little change) is [here](https://github.com/CIAvash/simple-c-parser/).

The used grammar exists in the documents directory. Along with other things that are produced from grammar: the LL(1) grammar after left factoring and left recursion removal, FIRST and FOLLOW sets and the parse table.

Take a look at the README.md for its usage and some dummy C code for using in scanner and parser.

Usage:

scanner:
```bash
./scanner.pl [file_name]
```

Output: Symbol Table (tokens)

parser:
```bash
./parser.pl [-s] [file_name]
```

Output: Table of parsing process

With -s switch you can also see the scanner's output.

[Simple C Parser on GitHub](https://github.com/CIAvash/simple-c-parser/)