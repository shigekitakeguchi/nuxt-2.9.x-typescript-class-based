# Nuxt.js（v2.9.x）+ TypeScript（Class-based）で環境を用意する
## はじめるにあたって
Vue CLIがかなり進化してきてNuxt.js使わなくてもけっこういけるようになったなと思ってます。  
とはいえ状況によってはやっぱSSRが必要になることもあったり規約というかルールを作っておいた方が何かといいよねっていうことは考えられますので、そういうときはさくっとNuxt.jsを選択してます。
最近だとほとんどの場合、すっかりTypeScirptを使っていますのでNuxt.jsでもTypeScriptで書きたいわけですがバージョンによって設定方法が変わってしまってうまくいかないことが多いです。  
ひとまずNuxt.jsの最新はNuxt.jsの日本語サイトだと2.8.Xってなってますが [https://ja.nuxtjs.org](https://ja.nuxtjs.org) 英語だと [https://nuxtjs.org](https://nuxtjs.org) 2.9.Xになってます。Yarnやnpmでなにも考えずにインストールするとv2.9.1（2019/8/29時点）です。
v2.9.0になってからオフィシャルドキュメント、ガイドもできたようで [https://typescript.nuxtjs.org/](https://typescript.nuxtjs.org/) それにあわせてなのかやり方がそれまでとまた変わってしまいました。

## インストールする手順
だいたいNuxt TypeScript [https://typescript.nuxtjs.org/](https://typescript.nuxtjs.org/)のGet Startedの手順でやればいいわけですがはじめてだとちょくちょくひっかかるところがありそうなのでメモがわりにレポジトリを用意してREADMEに残しておきます。  

### 必要なものあるかどうか確認

```
node -v
v10.15.1
```
まずはお決まりのNode.js入ってるか確認。本日のNode.js推奨版はv10.16.3なんですね。  
関わっているプロジェクトの関係からv10.15.1使ってます。たしかNodeはv8.9.0以上、npmは5.0.0以上って感じですね。  
[https://github.com/nuxt/nuxt.js/blob/dev/distributions/nuxt/package.json](https://github.com/nuxt/nuxt.js/blob/dev/distributions/nuxt/package.json)  
このあたりを参考にしていただければ。

### まずはNuxt.jsでプロジェクトを作成します。

Nuxt.jsのインストールの説明はnpxを使ってますね。npxはnpm v5.2.0以上だと特にインストール不要だったと思います。

```
npx create-nuxt-app <project-name>
```

```
yarn create nuxt-app <project-name>
```
今いるディレクトリにインストールしたい時はプロジェクト名を入れない感じでいきます。

```
yarn create nuxt-app
```

いくつかの質問に答えていきます。

```
? Project name
```

```
? Project description
```
```
? Author name
```

Yarnでもnpmでも好みで選びましょう。

```
? Choose the package manager (Use arrow keys)
❯ Yarn
  Npm
```

UIフレームワークは必要でなければNoneでいいでしょう。

```
? Choose UI framework (Use arrow keys)
❯ None
  Ant Design Vue
  Bootstrap Vue
  Buefy
  Bulma
  Element
  Framevuerk
  iView
  Tachyons
  Tailwind CSS
  Vuetify.js
```
サーバーフレームワークも必要でなければNoneでいいでしょう。

```
? Choose custom server framework (Use arrow keys)
❯ None (Recommended)
  AdonisJs
  Express
  Fastify
  Feathers
  hapi
  Koa
  Micro
```

Nuxt.js 公式モジュールですね。  
このあたりも必要に応じてインストールしてください。

* [Axios Module](https://axios.nuxtjs.org/)
* [Nuxt PWA](https://pwa.nuxtjs.org/)

```
? Choose Nuxt.js modules (Press <space> to select, <a> to toggle all, <i> to invert selection)
❯◯ Axios
 ◯ Progressive Web App (PWA) Support
```

なくても動きます。必要であればインストールしてください。

```
? Choose linting tools (Press <space> to select, <a> to toggle all, <i> to invert selection)
❯◯ ESLint
 ◯ Prettier
 ◯ Lint staged files
```

なくても動きます。必要であればインストールしてください。

```
? Choose test framework (Use arrow keys)
❯ None
  Jest
  AVA
```

サーバーサイドでレンダリングしたい場合はUniversal（SSR）を選んでください。  
こちらの記事などを参考にSingle Page AppかUniversalを選ぶといいと思います。

[Nuxt.jsを使うときに、SPA・SSR・静的化のどれがいいか迷ったら](https://qiita.com/nishinoshake/items/f42e2f03663b00b5886d)
[サーバサイドレンダリング](https://jp.vuejs.org/v2/guide/ssr.html)
> これまでに議論されたすべての側面を適切に構成するプロダクション向けのサーバーレンダリングに対応したアプリケーションの開発は難しい作業です。幸いにも、これをもっと簡単にすることを目指す優れたコミュニティプロジェクト Nuxt.js があります。Nuxt.js は、Vue エコシステムの上に構築された高レベルのフレームワークで、ユニバーサル Vue アプリケーションを作成するための非常に合理的な開発エクスペリエンスを提供します。

```
? Choose rendering mode (Use arrow keys)
❯ Universal (SSR)
  Single Page App
```

VS Codeを使っていたらインストールしてみてください。  
不要であれば後でプロジェクトのルートに追加されるjsconfig.jsonを消せばいいだけですね。

```
❯◯ jsconfig.json (Recommended for VS Code)
```

### このままではTypeScriptを使えません。
このままではTypeScriptが使えないです。いくつかの手順を踏む必要があります（そんなに難しくないです）。

Nuxtをアップデートします。現状では上記手順ですと2.0.0（2019/9/3現在）がインストールされます。  
ここでは2.9.0以上のやり方を説明します。  

```
yarn add nuxt
```
npmの場合

```
npm install --save nuxt
```

次に

```
yarn add --dev @nuxt/typescript-build
```
npmの場合

```
npm install --save-dev @nuxt/typescript-build
```

### nuxt.config.jsを編集
Nuxt.jsをインストールするとプロジェクトのルートにnuxt.config.jsが作成されます。  
ビルドモジュールの設定にインストールした `@nuxt/typescript-build` を追記します。

```json

export default {
  mode: 'universal',
  /*
  ** Headers of the page
  */
  head: {
    title: process.env.npm_package_name || '',
    meta: [
      { charset: 'utf-8' },
      { name: 'viewport', content: 'width=device-width, initial-scale=1' },
      { hid: 'description', name: 'description', content: process.env.npm_package_description || '' }
    ],
    link: [
      { rel: 'icon', type: 'image/x-icon', href: '/favicon.ico' }
    ]
  },
  /*
  ** Customize the progress-bar color
  */
  /*
  ** Global CSS
  */
  css: [
  ],
  /*
  ** Plugins to load before mounting the App
  */
  plugins: [
  ],
  /*
  ** Nuxt.js dev-modules
  */
  buildModules: [
    '@nuxt/typescript-build'
  ],
  /*
  ** Nuxt.js modules
  */
  modules: [
  ],
  /*
  ** Build configuration
  */
  build: {
    /*
    ** You can extend webpack config here
    */
    extend (config, ctx) {
    }
  }
}
```
初期状態では以下のようになっています。

```
buildModules: [
],
```
以下のように編集します。

```
buildModules: [
  '@nuxt/typescript-build'
],
```

### tsconfig.jsonの追加
TypeScriptを使うには `tsconfig.json` が必要になります。プロジェクトのルートに追加しましょう。

```
touch tsconfig.json
```
Nuxt.jsでTypeScriptを使うためのコンパイラオプションです。
このままの記述でも問題ないと思います。ルールや好みがある場合は必要に応じて設定を変えたり追記したりしましょう。  
[Compiler Options &middot; TypeScript](https://www.typescriptlang.org/docs/handbook/compiler-options.html)

```json
{
  "compilerOptions": {
    "target": "esnext",
    "module": "esnext",
    "moduleResolution": "node",
    "lib": [
      "esnext",
      "esnext.asynciterable",
      "dom"
    ],
    "esModuleInterop": true,
    "experimentalDecorators": true,
    "allowJs": true,
    "sourceMap": true,
    "strict": true,
    "noEmit": true,
    "baseUrl": ".",
    "paths": {
      "~/*": [
        "./*"
      ],
      "@/*": [
        "./*"
      ]
    },
    "types": [
      "@nuxt/types"
    ]
  }
}
```
### Class-based（クラススタイル）でTypeScriptを書きたい

このままでもTypeScriptは書けますがせっかくなのでClass-basedな書き方で書きましょう。  

```
yarn add vue-property-decorator
```
npmの場合

```
npm install --save vue-property-decorator
```

pages/index.vueはもともとこういう記述ですね（script部分だけ抜き出してます）。

```html
<script>
import Logo from '~/components/Logo.vue'

export default {
  components: {
    Logo
  }
}
</script>

```
Class-based（クラススタイル）ですと以下のように書けます。  
index.vueのclass名は何でも大丈夫なようですね。class名なので大文字からはじめてます。

```html
<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'

@Component({
  components: {
    Logo: () => import('~/components/Logo.vue')
  }
})
export default class Index extends Vue {
}
</script>
```
components/Logo.vueにはもともとscriptの記述はないですが以下を追記しました。

```html
<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'

@Component
export default class Logo extends Vue {}
</script>
```
日常的にClass-based（クラススタイル）で記述したい人は参考にしてみてください。  
[クラススタイル Vue コンポーネント](https://jp.vuejs.org/v2/guide/typescript.html#%E3%82%AF%E3%83%A9%E3%82%B9%E3%82%B9%E3%82%BF%E3%82%A4%E3%83%AB-Vue-%E3%82%B3%E3%83%B3%E3%83%9D%E3%83%BC%E3%83%8D%E3%83%B3%E3%83%88)

Nuxt.jsもここ最近のバージョンでTypeScriptのサポートが公式に組み込まれてきて問題なく使えるようになってきている印象です。  
Nuxt.jsでTypeScriptを使う設定の参考にしていただければと思います。
