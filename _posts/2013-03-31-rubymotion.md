---
layout: post
title: Info.plistの設定方法
date: 2013-03-31 22:14:53 +0900
tags: ruby rubymotion
---
続けざまにRubyMotionネタ。

info.plist触りたいのに、ファイルが無い！無い！

みたいな事になることがあります。

今回は、```UIStatusBar```を ```hidden``` にしたかった。

そんな時は、Rakefileを触ってあげればいいらしい。

```ruby
# Rakefile
Motion::Project::App.setup do |app|
  app.name = 'sample'
  app.info_plist['UIStatusBarHidden'] = true
end
```

簡単だった。
