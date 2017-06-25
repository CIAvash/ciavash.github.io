---
layout: post
title: 'MovieInfo - A web app for finding movie information and ratings'
---

I wanted to create something that makes it easy for me to see movie ratings.
I decided to create it as a SPA. In order to do so, I had to find a good framework.
I looked at a few well known frameworks, but did not like any of them!

I was going to give up, but then I saw [Elm](http://elm-lang.org/).
I had seen it being mentioned here and there, but I had never looked into it.
So I decided to give it a try and started reading the
[guide](https://guide.elm-lang.org/) and the [docs](http://elm-lang.org/docs).
I liked what I saw, so I did a bit more reading before starting the project.

[MovieInfo](https://ciavash.gitlab.io/MovieInfo/)
-------------------------------------------------

![MovieInfo - screenshot of a title]({{ site.baseurl }}/uploads/MovieInfo-title.jpg)

I wanted the project to be very simple and light, so I created a simple interface,
and used the [OMDb API](https://omdbapi.com/) to show the necessary information.

In addition to ratings from IMDB, Rotten Tomatoes and Metacritic,
I added an overall rating, which is the average of those ratings.

[MovieInfo](https://ciavash.gitlab.io/MovieInfo/) is released under GPLv3+
and its source code is available [here](https://gitlab.com/CIAvash/MovieInfo).