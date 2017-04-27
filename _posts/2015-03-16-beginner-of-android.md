---
layout: post
title: Android アプリ作りをなめちゃいかん
date: 2015-03-16 01:12:37 +0900
tags: android
description: iOS でアプリを作ったことがあったので、Androidのアプリづくりはなんとかなるだろうと思っていたんですが、思いのほか、前途多難な滑り出しでメンタル弱ってきたので、そのこころをブログにしました。
---
# Hello, Android

先週から、Androidアプリの開発が本格的に始まりました。

以前仕事で iOS アプリを作っていたことがあり、Android もまぁ、似たような感覚だろうと思っていました。

多少、機種差分があったり、OSバージョンが分散していたりと、ツライところもちらほら聞いていたけど、まぁそんなもんだろうと思っていました。

そんな心意気で、いざ開発を始めたわけです。

# マジでツライぞ, Android

開発が始まり、（当然ではあるけど）iOSと違うところがあまりにも多い。

あまりにツラすぎて、一週間が終わるころには、「辛い（からい）」も「ツライ」としか読めなくなるほど、疲れ果てていました。

なにより、ツライのがカメラ周り。

<!-- more -->

iOSだったら、めちゃくちゃ単純に実装するのであれば、本当にざっとですけど

```c
UIImagePickerController *picker = [[UIImagePickerController alloc] init];
picker.delegate = self;
picker.allowsEditing = YES;
picker.sourceType = UIImagePickerControllerSourceTypeCamera;

[self presentViewController:picker animated:YES completion:NULL];
```

これくらいの量で済むわけです。

一方の Android では、この記事に書くのを避けたくなるくらいの、大量のコードを書かなければいけない。

ざっと、やっただけでも2000行。クラスも10以上作ったような。

それもこれも、端末差分がでかい。 GPUの性能、端末ごとの写真の処理の仕方、カメラ自体の搭載具合。

その差分をクッションするようなことは、GoogleのAPIには用意されておらず、手元でなんとか頑張る。

そんな感じでした。

# 最初はこんなもんかも。

と、ツラツラと書いたのですが、まだ一週間。

iOSを始めた時も似たようなもんだったかな。。 すんなりと手を動かせるようになった記憶は色濃く残ってるけど、手が動かなかったときのことはあまり覚えてない。

あと、もうちょっと手を動かしていれば慣れるのだろうか。。慣れてくれ。。。

ということで、今週の対外的成果物はこちら。

- [users-permission と users-feature](http://qiita.com/tanukiti1987/items/7abe7a38a2595fe5b338)
- [Androidのスクリーンショットを1発で取得](http://qiita.com/tanukiti1987/items/943ee1d5b329054e22fc)
- [ToolBar(ActionBar)を自前で作りたいときに遭遇するエラーへの対処](http://qiita.com/tanukiti1987/items/e556ed9ef3aca76a49e9)

さぁ、今週も頑張るぞ！
