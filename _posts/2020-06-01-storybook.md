---
layout: post
title: Nuxt + Vuetify の構成で Storybook を導入する
date: 2020-06-01 22:00:00 +0900
tags: nuxt vuetify storybook
summary: Nuxt.js にて Vuetify を使っているプロジェクトにて、Storybook を導入する方法を案内します。Storybook は UIコンポーネントのカタログのようなもので、デザイナと開発者をつなぐ便利なツールなので、ぜひ使ってみてください！
---

![](https://skim.milk200.cc/images/tOroFBpiJAVtCwBrmimlZC7oduW1mbkM.jpg)

## Storybook を使っていく

[Storybook](https://storybook.js.org/) は UIコンポーネントを束ねるライブラリで、このツールごしにコンポーネントを眺めたり、コンポーネントに与えるパラメータを動かして、コンポーネントの変化を確認したりと、UIコンポーネントのカタログのようなものになります。

今回はこの Storybook を Nuxt.js + Vuetify を用いているプロジェクトに導入していく際の手順について、お伝えしていきます。

というのも、イチから準備しようとすると、あまりに手作業で追加する事項が多く、また体系的にまとめられているネット情報も少ないため、今回この記事を書くに至りました。

近い構成で [Storybook for Vue](https://storybook.js.org/docs/guides/guide-vue/) というドキュメントもあるのですが、こちらも参考程度に。という感じですね。

なお、今回はすでに Nuxt.js のプロジェクトがあることを前提として、説明を初めていきます。

また、今回使ったソースコードはこのブログの最下部に置いておきますので、ご参考ください。

## Storybook 関連パッケージを導入する

まずは、storybook 関連のパッケージを追加していきます。
`yarn` を使っていますが、`npm(npx)` でもコマンドがありますので、npm をお使いの方は適宜読み替えてコマンドを実行してください。

{% highlight html %}
$ yarn sb init --type vue
$ yarn add -D @storybook/addon-viewport @storybook/addon-notes @storybook/addon-knobs storybook-addon-vue-info
{% endhighlight %}

以下に、各アドオンの説明も記載します。

### @storybook/addon-viewport

![](https://skim.milk200.cc/images/oasb64cw4TpSDAdxCWJjjkne39GyAbrR.png)

[https://www.npmjs.com/package/@storybook/addon-viewport](https://www.npmjs.com/package/@storybook/addon-viewport)

storybook を起動後、プレビューの窓から表示するビューのサイズを切り替えることができるアドオンです。
レスポンシブに対応しているコンポーネントも多いと思うので、入れておきたいですね。

### @storybook/addon-notes

![](https://skim.milk200.cc/images/fFG2RZPG0RaAQurpFoSxdhjKI5oK1DxR.png)

[https://www.npmjs.com/package/@storybook/addon-notes](https://www.npmjs.com/package/@storybook/addon-notes)

各コンポーネントに対し、マークダウン形式でノートを残せるアドオンです。
Storybook 自体がドキュメンテーションにも向いているものだと思うので、Props などの調整以外にも、こういったノートを保存しておけると最高ですね！

### @storybook/addon-knobs

![](https://skim.milk200.cc/images/6cYEoa5nLBIyY40IqTQzilJbYrMw2pHU.png)

[https://www.npmjs.com/package/@storybook/addon-knobs](https://www.npmjs.com/package/@storybook/addon-knobs)

これが一番の目玉というか必須アドオンですね。
コンポーネントのプロパティーを動的に変えるためのアドオンになります。

画像では、 `dayOfTheWeekLabels` というプロパティーの先頭2つを日本語表記に変えています。
変更した瞬間に、プレビューされているコンポーネントにも瞬時に変更が反映されます。

これで、様々なプロパティを与えてどのように表示されるのかがだいぶ確認しやすくなります。

### storybook-addon-vue-info

![](https://skim.milk200.cc/images/H2D9igL2jZKBh8nDfCKkr1ctpFcGb5gZ.png)

[https://www.npmjs.com/package/storybook-addon-vue-info](https://www.npmjs.com/package/storybook-addon-vue-info)

ややノートに近い役割になりますが、定義している vue ファイルから、プロパティの要不要、デフォルト値などを出力してくれるアドオンになります。
ノートを書くのはしんどい。という場合にはひとまずこちらだけ入れておくというのもありですね。

## storybook の設定ファイルを用意する

ここからがプロジェクトごとにフリーハンドで用意していかなければならない項目になります。
一つ一つ用意していきましょう。

### .story/main.js

先程導入したアドオン諸々を指定するためのファイルを置きます。
また、このあとに用意していくことになる story ファイルへのパスを指定します。

今回は、`stories` 配下に置いた `stories` ファイルを読み込むような指定にしています。

{% highlight js %}
// .story/main.js

module.exports = {
  stories: ['../stories/**/*.stories.js'],
  addons: [
    '@storybook/addon-actions',
    '@storybook/addon-links',
    '@storybook/addon-viewport',
    '@storybook/addon-notes',
    '@storybook/addon-knobs',
    'storybook-addon-vue-info/lib/register',
  ],
}
{% endhighlight %}

### .story/webpack.config.js

Webpack 周りの設定を追加していきます。
以下に示しているのは、`ts` `css` `sass` `scss` `vue` を代表とした設定になります。
もしプロジェクトで上記以外のファイルも使っている場合には、適宜書き換えが必要になります。

個人的にはここでボロボロにハマったので、皆さんのお役に立てればいいのですが。。

{% highlight js %}
//.story/webpack.config.js

const path = require('path')
const rootPath = path.resolve(__dirname, '../')

module.exports = async ({ config, mode }) => {
  mode = 'development'

  config.module.rules.push({
    test: /\.(otf|eot|svg|ttf|woff|woff2)(\?.+)?$/,
    loader: 'url-loader',
  })

  config.module.rules.push({
    test: /\.css/,
    use: [{ loader: 'postcss-loader', options: { url: false } }],
  })

  config.module.rules.push({
    test: /\.ts/,
    use: [
      {
        loader: 'ts-loader',
        options: {
          appendTsSuffixTo: [/\.vue$/],
          transpileOnly: true,
        },
      },
    ],
  })

  config.module.rules.push({
    test: /\.vue$/,
    loader: 'storybook-addon-vue-info/loader',
    enforce: 'post',
  })

  config.module.rules.push({
    test: /\.s(c|a)ss$/,
    use: [
      'style-loader',
      'css-loader',
      {
        loader: 'sass-loader',
      },
    ],
  })

  config.resolve.extensions = ['.js', '.vue', '.json']
  config.resolve.alias['~'] = rootPath
  config.resolve.alias['@'] = rootPath

  return config
}
{% endhighlight %}

### .story/preview.js

`config.js` という命名でも良いみたいなのですが、私のプロジェクトでは `preview.js` という名前で設定ファイルを置いています。
以下に記すのが、今回、Nuxt + Vuetify を使う上で重要なコードになります。

一度コードを示した上で、解説していきます。

{% highlight js %}
// .story/preview.js

import { configure, addDecorator } from '@storybook/vue'
import { withKnobs } from '@storybook/addon-knobs/vue'
import { withInfo } from 'storybook-addon-vue-info'
import { action } from '@storybook/addon-actions'

import Vue from 'vue'
import Vuex from 'vuex'

import Vuetify from 'vuetify'
import { VApp, VContent } from 'vuetify/lib'
import colors from 'vuetify/es5/util/colors'
import 'vuetify/dist/vuetify.min.css'

Vue.use(Vuex)
const vuetifyOptions = {}

Vue.use(Vuetify, {
  iconfont: 'mdi',
  customVariables: ['~/assets/variables.scss'],
  theme: {
    dark: true,
    themes: {
      light: {
        primary: colors.purple,
        secondary: colors.grey.darken1,
        accent: colors.shades.black,
        error: colors.red.accent3,
      },
      dark: {
        primary: colors.blue.darken2,
        accent: colors.grey.darken3,
        secondary: colors.amber.darken3,
        info: colors.teal.lighten1,
        warning: colors.amber.base,
        error: colors.deepOrange.accent4,
        success: colors.green.accent3,
      },
    },
  },
})

// nuxt-link を action に送る
Vue.component('nuxt-link', {
  props: ['to'],
  methods: {
    log() {
      action('link target')(this.to)
    },
  },
  template: '<a href="#" @click.prevent="log()"><slot>NuxtLink</slot></a>',
})

// automatically import all files ending in *.stories.js
const req = require.context('../stories', true, /.stories.js$/)
function loadStories() {
  req.keys().forEach(filename => req(filename))
}

configure(loadStories, module)
addDecorator(() => ({
  vuetify: new Vuetify(vuetifyOptions),
  components: { VApp, VContent },
  template: `<v-app><v-content><story/></v-content></v-app>`,
}))
addDecorator(withKnobs)
addDecorator(withInfo)
{% endhighlight %}

上記コードの解説になりますが、このファイルで Vuetify まわりを import します。
`VApp` や `VContent` はファイル下部にある `addDecorator` で使うことになります。

ファイル中盤、Vuetify に初期設定の情報を付与しつつ、`Vue.use` します。

その後、 `addDecorator` でプレビュー時にコンポーネントが `VApp` と `VContent` でラップされるように指定してあげます。

ここまでの設定ができると、 Vuetifyをベースにしたコンポーネントもほぼほぼ表示されることになると思います！
（アイコンが表示されないと思うので、以下に続きます。）

#### おまけ: nuxt-link をクリックしたときに、アクションに送信する

ファイル中盤にある `nuxt-link` 関連の設定は、コンポーネントに含まれる `nuxt-link` をクリックしたときに、storybook の actions に送信されるようにしてあげます。

ちょっとしたおまけ設定ですが、クリックの挙動まで見るのであれば、便利かなと思います。

### .story/preview-head.html

前述しましたが、ここまでの設定だとアイコンフォントが表示されていないと思うので、`.story/preview-head.html` というファイルを用意して、そこにアイコンフォントを表示させるための link タグを置きます。

この `preview-head.html` というファイルは、プレビューを表示する際、その窓にて配置される html になります。
スタイルシートだけでなく、プレビュー時に当てたい js ファイルなどあればこのファイルに置いてあげることで、プレビュー時の挙動を制御できるかと思います。

{% highlight html %}
<link
  href="https://fonts.googleapis.com/css?family=Roboto:100,300,400,500,700,900&display=swap"
  rel="stylesheet"
/>
<link
  href="https://cdn.jsdelivr.net/npm/@mdi/font@3.x/css/materialdesignicons.min.css"
  rel="stylesheet"
/>
{% endhighlight %}

## story を追加する

さて、もうそろそろ終盤です。

Storybook でコンポーネントを見られるように、まず story ファイルを用意していきます。
今回は、 `~/components/WeatherCard.vue` があるものとして話を進めます。

### stories/WeatherCard.story.js

もともと用意しているコンポーネントをもとに以下のようなファイルを置きます。

{% highlight js %}
// stories/WeatherCard.story.js

import { storiesOf } from '@storybook/vue'
import { array } from '@storybook/addon-knobs/vue'
import WeatherCard from '@/components/WeatherCard.vue'

storiesOf('Components/Vuetify', module).add(
  'WeatherCard',
  () => ({
    components: { WeatherCard },
    template: `<weather-card :day-of-the-week-labels="dayOfTheWeekLabels"/>`,
    props: {
      dayOfTheWeekLabels: {
        type: Array,
        default: array('dayOfTheWeekLabels',
          ['SU', 'MO', 'TU', 'WED', 'TH', 'FR', 'SA']),
      },
    },
  }),
  {
    info: true,
    notes: `
        # WeatherCard

        ## Props
        * dayOfTheWeekLabels
          * Array
            * 曜日の表示形式
      `,
  }
)
{% endhighlight %}

`storiesOf` というメソッドにて、パスを決めつつ、コンポーネントを追加します。
書き方については、 vue とかなり近い書き方だと思うので、詳しくは割愛します。

また、冒頭で導入したノートのアドオンも上記の様に使うことができます！

### stories/index.stories.js

さて、上記で作った story ファイルを stories ファイルに import し、storybook に表示できるようにします。

{% highlight js %}
// stories/index.stories.js

import './WeatherCard.story'
{% endhighlight %}

コンポーネントを追加するごとにここにファイルを追加していくもよし、自動で読み込まれるように書き方を工夫しても良しですね。

## storybook を起動する

ここまできたら、めでたく storybook を起動しましょう。

```
$ yarn storybook
```

![](https://skim.milk200.cc/images/G0oj6hXukOHKe5wm7dxobv6FAGFxA7ZA.png)

👍

あとはどんどんコンポーネントを足していき、快適な開発ライフをお過ごしください〜。

今回この記事を書くにあたり使ったコードは

[https://github.com/tanukiti1987/vuetify_storybook](https://github.com/tanukiti1987/vuetify_storybook)

こちらにおいています。細かめにコミットを分けていますので、部分的に見ていただくこともできるかと思います。
ぜひ、ご参考ください 🙏
