---
layout: post
title: colorful-cursor というatom package をリリースしました
date: 2016-01-03 01:00:00 +0900
tags: atom
summary: atom のpackage を何か作ってみたくて、colorful-cursor というのを作ってみました。プログラミング中にカーソルの色がどんどん変わっていく拡張をするための package です。 その package を作るがてら、苦労したところなどをまとめています。
---

![](https://skim.milk200.cc/20160103_colorful_cursor/colorful-cursor.gif)

## colorful-cursor

atom で何か拡張書いてみたいなーということで、作ってみました。

キーボードで何かタイピングするごとに、カーソルの色が変わるモノです。

このpackageでは、カーソルのカラーコードを保持しておき、打鍵があるごとにその `KeyCode` を末尾に16進数で結合し、新しいカーソルの色を決定するすごく簡単な仕組みで動いています。

package と ソースコードは以下より参照ください。

[colorful-cursor (atom.io)](https://atom.io/packages/colorful-cursor)

[tanukiti1987/colorful-cursor (github.com)](https://github.com/tanukiti1987/colorful-cursor)

### 開発の敷居

atom の package の開発はすごく敷居が低いように感じました。

2016年、静かに終わりが近づいていると噂されている coffeeScript を始め、ES6 でも開発が行えます。

また、package のテンプレートについても、menu から `Packages -> Package Generator` から簡単にできます。

package が開発完了すれば `apm publish minor` とターミナルに撃ちこめば自動でリリースされるという手軽さ。

### 苦労点もいくつか

ドキュメントについては、[こちら](https://atom.io/docs/) から参照できます。

ただ、個人的には用意されているAPIやコールバックの使い方は慣れるまでちょっと苦労しました。

そして、今もまだ理解不足だと思うところもあり、この辺はいくつか開発してみたりして試さないとなんとも。といったところでしょうか。

React も近辺の知識もがんばって勉強していかないとなーと思った次第でした。

## 最後に

開発中は、主にプログラムを組みながら、このPackageの動きを確認していたのですが、このブログを書いていて気がついたことが一つ。

__日本語打ち込むと、カーソルの色が固定される！！！__

全く日本語打ってなかったから気が付かなかった。。（しかも色が見にくいｗ）

あとで直したいところですが、プログラミングをしていると、カーソルの色がチカチカ変わって可愛いです。

すこしづつ直して、愛でていこうと思いますので、皆様もぜひ使ってみてください mm

### 参考文献

- [Atomパッケージを作る - ワード境界を日本語対応させるパッケージ: japanese-word-selection](http://tbd.kaitoy.xyz/2015/08/21/japanese-word-selection/)
- [Atomのパッケージを作ってみた](http://takezoe.hatenablog.com/entry/20140823/p1)
