---
layout: post
title: Androidのスクリーンショットを1発で取得
date: 2015-03-11 00:00:00 +0900
tags: Android
---

Androidの開発をするに際して、よく使うであろうスクリーンショットの取得。
社内の知見があったので、使ってる際の作業ログ。

#### 元ネタ

http://techlife.cookpad.com/entry/2014/12/17/182050

## homebrew で android-sdk をインストールする

```
brew install android-sdk
```

コマンドラインから作業をすることも多いし、AndroidStudio経由で `android-sdk` をインストールするよりもオススメ。

## スクリーンショットコマンド当たりにPATHを通す

brew で sdk をインストールすると、 `/usr/local/opt/` 以下に sdk が配置されます。

今回使用する `screenshot2` というコマンドは `/usr/local/opt/android-sdk/tools` 以下にあるので、お好みにもよりますが、この辺にPATHを通しておきます。

## alias をはる

ここまでで `screenshot2` というコマンドが使えるようになって、

```
screenshot2 ~/screenshot.png
```

とかやると、接続中の端末のスクショが取れる用になります。

ここで元ネタより、

```
alias screenshot='screenshot2 $TMPDIR/screenshot.png; open $TMPDIR/screenshot.png'
```

みたいなエイリアスをお使いのシェルに追加しておくと、スクショをとって、プレビューで開くみたいなことができて、かなり便利！


Android のスクショ撮るのは個人的にはかなり面倒だと思っていたので、これはだいぶ捗ります。
