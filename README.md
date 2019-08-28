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


```
? Choose Nuxt.js modules (Press <space> to select, <a> to toggle all, <i> to invert selection)
❯◯ Axios
 ◯ Progressive Web App (PWA) Support
```

```
? Choose linting tools (Press <space> to select, <a> to toggle all, <i> to invert selection)
❯◯ ESLint
 ◯ Prettier
 ◯ Lint staged files
```

```
? Choose test framework (Use arrow keys)
❯ None
  Jest
  AVA
```
```
? Choose rendering mode (Use arrow keys)
❯ Universal (SSR)
  Single Page App
```
```
❯◯ jsconfig.json (Recommended for VS Code)
```