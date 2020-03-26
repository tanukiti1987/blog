---
layout: post
title: RubyMotion with TravisCI
date: 2013-05-19 00:00:00 +0900
tags: RubyMotion TravisCI
---

継続的インテグレーションの味方、TravisCIをRubyMotionのプロジェクトにも対応させる方法です。

すんごく簡単。

プロジェクトの直下に `.travis.yml` を配置。

んで中身に

```yml
language: objective-c
before_install:
    - (ruby --version)
script: "(bundle install) && (bundle exec rake clean) && (bundle exec rake spec)"
```

を書いてあげてgitにpushすればOK!

また、最近RubyMotionはOSXアプリも作れるようになってます。そちらのスペックも同時に動かすのであれば、

`(bundle exec rake clean) && (bundle exec rake spec osx=true)` も更に加えてあげると幸せになれます。