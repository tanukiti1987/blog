---
layout: post
title: "raspberryPiでAirPlay"
date: 2014-11-16 18:16:07 +0900
comments: true
categories: [raspberryPi]
---

![raspberryPi](https://skim.milk200.cc/20141116_raspberrypi/raspberryPi.jpg)

# raspberryPi をひと通り楽しむ

会社の人からもらった raspberryPi（以下、ラズパイ）。
正直いうと、しばらく触り始めのコストが高くて、触れてなかったんです。

でも、ちょっとだけ時間ができたので、いじり始めたら結構楽しい。

定番のLEDチカチカをしてみたり、部屋の照度や、温度を測ってみたり、ひと通り楽しんでみました。

けど、あんまり実用的じゃない。

じゃあ、ラズパイで何しよう。ってことで、[RaspBMC](http://www.raspbmc.com/)を使って、部屋の中にAirPlayの環境を実現してみました！

<!-- more -->


# さながら格安AppleTVだ！

導入はめちゃくちゃ簡単。

- RaspBMCをサイトに書いてある通りにインストール
- OverClockなどのパフォーマンスチューニング
- 設定からAirPlayを有効にする

以上！ rasbpbian などのOSの上で動かそうとすると、たぶんもうちょっとやることあるんですが、個人的にはもうこの使い方だけで構わなそう。

最後に、iPhone/iPad などに [XMBC remote](https://itunes.apple.com/us/app/unofficial-official-xbmc-remote/id520480364) をインストールすれば、キーボードやマウスなどをラズパイに付けなくても良くなる。

iPadでhuluをAirPlayしたり、iPhoneで音楽をAirPlayしたり。

今までAirPlay使ってこなかったですが、これはかなりライフチェンジング。

しかも、必要なのはラズパイ一式とWiFiのUSBコネクタのみ。

お値段もAppleTVほど高くならない。

動作は若干不安定なところもありますが、遊び終わったラズパイがあれば、一回試してみる価値はあるかもしれません。
