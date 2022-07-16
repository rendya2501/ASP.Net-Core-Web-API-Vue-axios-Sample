# ASP.Net Core Web API + Vue axios 通信サンプル

Vueのプロジェクト作成の方法のまとめと一捻りしてASP.Netでサーバーを立ててaxiosでアクセスする最小実装をまとめたサンプル。  
後々詳しくまとめていく。  
今は時間がないので、適当なリンクととりあえず、できたものを上げる。  

全体的な方針はここ参考にした。  
[vue.js + typescript = vue.ts ことはじめ](https://qiita.com/nrslib/items/be90cc19fa3122266fd7)  

axiosについてはここらへん。  
[Vue3とaxiosで外部サイトにアクセス](https://akkunblog-happy-life.com/vue3-20/)  
[axios超簡易サンプル](https://qiita.com/nitakaho/items/6034a35091c16710bcbc)  

---

## 開発サーバのプロキシ設定

[Vue CLI3のDevServerでWebSocketを使う](https://qiita.com/dbgso/items/4bbfa52d99cae6c547a4)  

確か実務では[[vue.config.js]devServerのproxyが動作しない](https://qiita.com/mikene_koko/items/767e5cd5cfb31e93f095)のページを参考にして、こんな風にプロキシの設定したけど、  
単純にプロキシ立てるだけなら2番目の例で十分だった。  

``` js : 実務のweb.config.js
module.exports = {
  devServer: {
    https: true,
    port: 8080,
    disableHostCheck: true,
    proxy: {
      '/api': 
      {
        target: 'http://localhost:61207/~~~/~~~',
        changeOrigin: true,
        pathRewrite: { "^/api": "" },
      }
    }
  }
}
```

``` js : web.config.js
module.exports = {
  devServer: {
    proxy: 'http://localhost:4000'
  }
}
```

---

## 嵌ったポイント

- クラス記法とオブジェクト記法の違い  
- Vue3ではvue-property-decoratorを使った書き方は古いorサポートされていない？  
- axiosのインポートは中括弧を付けるとだめ。  
- CORSの解決,プロキシサーバーの立て方全般  
- Vue3での実装  

---

## 参考リンク集

[【Vue.js】Vue + typescript について (vue-class-component, vue-property-decorator って何？)](https://miyablo.sakura.ne.jp/home/development/vue-typescript/)  

[簡単な例で始めるVue3でTypeScript入門](https://reffect.co.jp/vue/vue3-typescript#i-2)  
[【2021年版】Vue.js + TypeScriptの開発スタイル](https://tech-blog.rakus.co.jp/entry/20210901/frontend)  
[はじめてのvue-property-decorator (nuxtにも対応）](https://qiita.com/simochee/items/e5b77af4aa36bd0f32e5)  
[Should anything concern me if I want to upgrade from vue2 with `vue-property-decorator` (class style) to vue3?](https://stackoverflow.com/questions/69545935/should-anything-concern-me-if-i-want-to-upgrade-from-vue2-with-vue-property-dec)

[Vue.jsの環境構築](https://future-architect.github.io/typescript-guide/vue.html)  

[type 'typeof import( node_modules/vue/dist/vue )' is not a constructor function typeについて](https://winmundo.com/vue-js-vue-3-typescript-class-component-type-typeof-import-node_modules-vue-dist-vue-is-not-a-constructor-function-type/)
>vue.js – Vue 3 Typescriptクラスコンポーネント–タイプtypeof import（…/ node_modules / vue / dist / vue）はコンストラクター関数タイプではありません  
>この問題に基づいて、そのデコレータは必要なく、バージョン3ではインポートが異なります。  
