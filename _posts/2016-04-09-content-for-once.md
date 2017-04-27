---
layout: post
title: content_for_once というgemをリリースしました
date: 2016-04-09 21:35:29 +0900
tags: ruby gem
description: content_for_once という rails の plugin があったのですが、現在では gem によるライブラリの配布が一般的になってきています。 今回はその content_for_once を gem 化したことについて、使いかたを合わせてご紹介します。
---

Railsで、viewファイルに対して、`javascript_include_tag` や `stylesheet_link_tag` を多重に読み込んでしまうような書き方をしてしまうことって、ありますよね。

重複して css や js ファイルを読み込んでしまうことで、スタイルが壊れてしまったり、jsの動きがおかしくなってしまったり。。。などなど、困ることも多いです。

content_for_once はそれを解決するための gem です。

## content_for_once

`content_for_once` というフレーズをグーグルなどで検索していみると、 [この記事](http://blog.s21g.com/articles/203) にあたるのですが、私の記事で紹介する内容は、呼び名こそ同じものの、少し動きを変えております。

先ほどの記事では Rails に対してライブラリを追加するとき `script/plugin` というコマンドによりライブラリを追加するのが標準だった頃の内容でした。(ボクはその時代のRailsをよく知らない。。)

現在ではみなさんもお馴染みのgemによるライブラリの配布が主流になり、この配布の形に乗せて、似たようなものを使いたい。という思いがありました。

https://rubygems.org/gems/content_for_once

命名に関してですが、`content_for_once` という名前でプラグインをブログ記事を書かれている方がいたのですが、`content_for_once` いい名前だよな。。というのと、オリジナルの `content_for_once` はpluginの形で公表されているものの、ソースコード自体はもうリンク切れになっており、流通も少なそうな雰囲気を受けたので、オリジナル作者の方に連絡をして、名前やら処理の内容を変更することに許可を頂き、`content_for_once` という名前をつけました。

## 使いかた

```haml
-# app/views/layout/application.html.haml
= yield :css

-# articles/index.html.haml
- @articles.each do |article|
  = render 'article', article: article

-# articles/_article.html.haml
- content_for_once :css do
  = stylesheet_link_tag 'article'

.article
  .title= article.title
```

こんな感じに、 `index.html.haml` と `_article.html.haml` に同じcssを読み込むような記述を書いたとしても、従来の `content_for` では2つの `<link rel="stylesheet" href="article.css">` が挿入されてしまうところ、 `content_for_once` を使えば、1度だけの挿入で済むようになります。

## まとめ

もしよろしければ、ご利用頂いたり、PRやissue などでアドバイスいただければと思います mm
