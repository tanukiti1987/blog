---
layout: post
title: I Just release "jbuilder-jets" gem
date: 2020-05-01 23:30:00 +0900
tags: ruby jets serverless
summary: I've released a gem called jbuilder-jets that makes it easy to introduce Jbuilder with Jets, Ruby's Serverless Framework. Jets is a framework that also has a Rails feel to it, so if you're new to Rails, give it a try!
---

The title says it all, but we've released a gem for using Jbuilder with Jets.

[https://rubygems.org/gems/jbuilder-jets](https://rubygems.org/gems/jbuilder-jets)

I started to use Jets at work, but I couldn't use Jbuilder by default when using Jets in API mode, so I wrote this gem because I got frustrated when I wrote the view template.

The contents are very simple. you don't need to write the configuration of Jbuilder in `config/initializers` by yourself. It has only a few merits, but I wanted to reduce small stumbles, so I reached the release.

By the way, the original story is below.

[https://community.rubyonjets.com/t/rendering-as-xml-doesnt-work/80/2](https://community.rubyonjets.com/t/rendering-as-xml-doesnt-work/80/2)

## By the way, what is Jets?

![](https://skim.milk200.cc/2020/05/01/jets-logo.png)

[Jets: The Ruby Serverless Framework](https://rubyonjets.com/)

Jets is a serverless framework for Ruby, specifically, it uses AWS Lambda to achieve serverlessness.

The framework itself is modeled after Rails, and you can touch Routes, Controller, View, Config, etc. almost the same as Rails way.

You can also execute commands on the command line like `jets server` or `jets db:migrate` in Rails style.

There is also a good amount of documentation by the author, and if you have a problem, you can read the documentation or discuss it with the community I mentioned earlier.

It's been a while since Jets was released, and there's a lot of GitHub Star, and the maintenance is stable, so it's a framework I'm a little concerned about.

## I'd like to write more articles

There are a lot of articles about Jets on the Internet, but some of them are a bit confusing if you try to use them seriously.

Most of them can be solved, but I don't feel like I've done much in the way of know-how, so I'd like to continue writing in that area.

I think the API mode of Rails is also very light, but the API mode of Jets is very light even if you look at the dependency of gem, the front end is left to other frameworks, I want to make an API quickly. It seems to come in handy when you're looking for a new way of doing things.

I hope you'll give it a try, too.
