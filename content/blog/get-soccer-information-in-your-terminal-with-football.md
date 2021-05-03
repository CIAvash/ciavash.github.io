---
date: "2016-05-12T00:00:00Z"
title: 'Get football information in your terminal with football'
categories: [Project, CLI]
tags: [CLI, Football, Information, Football-Data]
aliases:
    - /blog/2016/05/12/new-project-get-soccer-information-in-your-terminal-with-football.html
---

![Football Leagues](/img/football-leagues.png)

[App::Football](https://gitlab.com/CIAvash/App-Football) is a command line program I wrote in [Raku](https://raku-lang.ir/en).
`football` lets you access information regarding football(soccer!) teams, leagues, tables, fixtures, scores and players.

It uses another module I wrote called [WebService::FootballData](https://gitlab.com/CIAvash/WebService-FootballData) which is a Raku interface for
[football-data.org](http://football-data.org) API.

To install App::Football, you need to first install [Raku](https://raku-lang.ir/en/downloads/)
and [Zef](https://github.com/ugexe/zef), then run:

```bash
zef install App::Football
```

The [README](https://gitlab.com/CIAvash/App-Football/blob/master/README.md) file has some useful examples,
but here are more examples and screenshots:

```bash
football --team=bayern --fixtures --timeframe=p30 --venue=away
```

![Football - Bayern away fixtures](/img/football-bayern-away-fixtures.png)

```bash
football --team=mancity --players
```

![Football - Mancity players](/img/football-mancity-players.png)

```bash
football --league=pl --table --matchday=37
```

![Football - PL matchday 37 table](/img/football-pl-table-matchday-37.png)