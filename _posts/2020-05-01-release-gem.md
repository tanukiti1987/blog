---
layout: post
title: jbuilder-jets というgemをリリースしました
date: 2020-05-01 23:30:00 +0900
tags: ruby jets serverless
summary: Ruby の Serverless Framework である Jets で Jbuilder が簡単に導入できる jbuilder-jets という gem をリリースしました。 Jets は Rails の雰囲気も感じさせるフレームワークで、Rails 慣れしてる方はぜひ試してみてください！
---

タイトルがすべてを物語ってしまっていますが、 Jets で Jbuilder を使うための gem をリリースしました。

[https://rubygems.org/gems/jbuilder-jets](https://rubygems.org/gems/jbuilder-jets)

仕事で、Jets 使ってみよう！というところから使い始めたのですが、API モードで Jets を使用する際に Jbuilder がデフォルトでは使えず、view template を書くときに歯がゆい気持ちになってしまったため、この gem を書きました。

中身は非常にシンプルで、 `config/initializers` に Jbuilder の設定を自分で書かなくて済む。くらいのメリットしかありませんが、小さいつまずきを減らしたいなってことで、リリースに至りました。

なお、元ネタは

[https://community.rubyonjets.com/t/rendering-as-xml-doesnt-work/80/2](https://community.rubyonjets.com/t/rendering-as-xml-doesnt-work/80/2)

この辺りから持ってきています。

## ところで、Jets って何

![](https://skim.milk200.cc/2020/05/01/jets-logo.png)

[Jets: The Ruby Serverless Framework](https://rubyonjets.com/)

Jets は Ruby のサーバーレスフレームワークで、具体的には AWS Lambda を用いてサーバーレスを実現するフレームワークになります。

フレームワーク自体は、Rails に倣ったものになっており、Routes や Controller, View, Config などほとんど Rails と同じ感じで触ることができます。

コマンドラインも同じく `jets server` であったり、`jets db:migrate` みたいな感じで Rails ライクにコマンドを実行することができます。

作者によるドキュメントも充実しており、なにかちょっと詰まるところがあれば、ドキュメントを読むか、先程記載したコミュニティでディスカッションされていることが多いです。

Jets はリリースされてから、しばらく時間が経っており、GitHub Star も多く、メンテナンスも安定してされており、ちょっと気になっているフレームワークです。

## 「やってみた」を超える記事も書いていきたい

インターネットには「やってみた」系のJetsに関する記事はとても多いのですが、いざ本気で使おうとするとちょっと困るという部分もちらほらと出てきています。

解決可能な部分がほとんどですが、あまりノウハウとして外に出ていないような感じもするので、その辺りも引き続き書いていければなと思っています。

Rails のAPIモードも非常に軽量かと思いますが、Jets のAPIモードは gem の依存関係を見てもとても軽く、フロントエンドは他のフレームワークにお任せして、ささっとAPIを作りたい。というときにかなり重宝しそうな感じがしています。

ぜひぜひ、みなさんもお試しあれ。