# sample-static-vue

## About
* Vue.js+Nuxt.js学習用リポジトリ
* Firebase Hosting上にホスティングして稼働中

### Note

#### Vueファイル

|vue|用途|
|---|---|
|index.vue|トップページ|
|nlpapi.vue|Cloud NLP APIにPOST(axios勉強用)|
|snippets.vue|試し書き用|
|automl.vue|~~Cloud AutoML NLPにPOST~~(工事中)|
  
  
#### `.env`書き方
```
API_KEY=hogehuga
```

## 参考書
* [Vue.js&Nuxt.js超入門](https://www.shuwasystem.co.jp/book/9784798056593.html)
  


  
## ビルド系のコマンド、備忘メモ
### npm系
* 参考
  * https://ja.nuxtjs.org/docs/2.x/get-started/commands/
```bash
# install dependencies
$ npm install

# serve with hot reload at localhost:3000
$ npm run dev

# generate static project
$ npm run generate

# build for production and launch server
$ npm run build
$ npm run start

```
  

### Firebase
```bash
# login
firebase login
# init
firebase init

###

# emulator
firebase emulators:start

# deploy
firebase deploy
firebase deploy

firebase deploy --only hosting
```
