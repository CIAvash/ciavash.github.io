---
layout: post
title: '[New Project] Get football information in your terminal with football'
---

![Football Leagues]({{ site.baseurl }}/uploads/football-leagues.png)

[App::Football](https://gitlab.com/CIAvash/App-Football) is a command line program I wrote in [Perl 6](https://perl6.org/).
`football` lets you access information regarding football(soccer!) teams, leagues, tables, fixtures, scores and players.

It uses another module I wrote called [WebService::FootballData](https://gitlab.com/CIAvash/WebService-FootballData) which is a Perl 6 interface for
[football-data.org](http://football-data.org) API.

To install App::Football, you need to first install [Perl 6](https://perl6.org/downloads/)
and [Zef](https://github.com/ugexe/zef), then run:

```bash
zef install App::Football
```

The [README](https://gitlab.com/CIAvash/App-Football/blob/master/README.md) file has some useful examples,
but here are more examples and screenshots:

```bash
football --team=bayern --fixtures --timeframe=p30 --venue=away
```

![Football - Bayern away fixtures]({{ site.baseurl }}/uploads/football-bayern-away-fixtures.png)

```bash
football --team=mancity --players
```

![Football - Mancity players]({{ site.baseurl }}/uploads/football-mancity-players.png)

```bash
football --league=pl --table --matchday=37
```

![Football - PL matchday 37 table]({{ site.baseurl }}/uploads/football-pl-table-matchday-37.png)