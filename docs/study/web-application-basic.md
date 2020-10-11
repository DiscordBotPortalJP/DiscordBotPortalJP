# Webアプリケーション開発基礎編

## Webアプリケーションの仕組み
- ブラウザは HTML と CSS と JavaScript しか対応してない
- サーバー側で諸々処理して、3種ファイルを渡してブラウザにお任せ
- Webブラウザ ↔ Webサーバー ↔ APサーバー ↔ Webアプリケーション
- [超絶初心者のためのフロント入門（HTML、CSS、JavaScript） - Qiita](https://qiita.com/shuntaro_tamura/items/c9b2fec0f3a9f7d1e987)

### HTML
- [HTML の基本 - ウェブ開発を学ぶ - MDN](https://developer.mozilla.org/ja/docs/Learn/Getting_started_with_the_web/HTML_basics)
- Hypertext Markup Language
- Webサイトの本体。主にレイアウトを決めるための言語。

### CSS
- Webページのデザインを司っている

### JavaScript
- Webページに動きを作ってくれる
(例: 画像をクリックしたらタイトル文字列を変える)

## ネイティブアプリケーション
- PC/スマホにインストールするアプリケーション
    - Swift(iOS),Kotlin(Android),Electron(PC) など
- Webアプリケーションと対になる存在

## 各種担当領域
(これらのことをすべてやる人は「フルスタックエンジニア」と呼ばれたりする)

### フロントエンド(クライアントサイド)
- 主にユーザが触る画面を担当
- HTML,JavaScript,CSS,jQuery,Vue&Nuxt,React&Next,Angular など

### バックエンド(サーバーサイド)
- 主にフロントエンドに渡すデータの処理を担当
- PHP(Laravel),Ruby(Rails),Python(Django,Flask,FastAPI),Node(Express) など

##### Webフレームワーク
- ライブラリをまとめたもの
- ライブラリとの違いは「書き方を強制されるか否か」
- ライブラリは拡張して使うものだがフレームワークは決められた書き方に沿うほうがやりやすい

### インフラ
- Webアプリケーションの開発環境/動作環境を担当
- Linux,Nginx,Docker,MySQL,PostgreSQL,AWS,GCP など

## 簡単に作ってみる
- 画面を HTML,JavaScript,CSS で作る
- サーバーからデータを渡してみる

## 余談：最近のWebアプリケーションの構成について
1. バックエンド側で画面を作りきってユーザに渡すパターン
    - バックエンド中心 -> データと画面を混ぜてユーザに渡す
2. SPA/API駆動
    - フロントエンド中心 -> APIを叩いてデータを取りに行く
