---
layout: post
title: users-permission と users-feature
date: 2015-03-27 00:00:00 +0900
tags: Android
---

Android の開発を初めて、手が止まったところを書いていく。

今回は AndroidManifest.xml について。

## 似たような設定が2つある

users-permission は、アプリが利用する `権限` をユーザーに許可してもらうための宣言として心得ていましたが、その言葉に近い users-feature というのがあるということが、他のAndroidアプリを見てみると分かりました。

これら2つの名前から察するに、ほとんど機能は似ていそうですが、少しだけ違う模様。

## なにが違うのか

答えは[ココ](http://developer.android.com/guide/topics/manifest/uses-feature-element.html#permissions) に書いてあるのですが、一応ざっとメモ。

### users-permission

冒頭述べたように、ユーザーがアプリをインストールする時に、アプリがOSの機能へアクセスすることへの許可を求める機能の種類を記述する。
OKの上、インストールしてもらえれば、アプリからその機能を使用できる。

### users-feature

対する feature は端末自身が持っているべき機能を記述するところ。 例えばカメラを使用する際、

```xml
<uses-feature android:name="android.hardware.camera"/>
<uses-feature android:name="android.hardware.camera.autofocus"/>
```

という記述を加えると、カメラ機能を持ち、更にオートフォーカスの機能を持っている端末のみが、このアプリをインストールできることになる。

それぞれの `feature` に `android:required="false"` を加えてあげることで、必ずしもこの制限を加えずにインストールできるようになる模様。

と、簡単にまとめたものの、詳細はdocumentを読むべし！
