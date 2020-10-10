# JavaScript基礎編

## JavaScriptとは

- プログラミング言語
- (ほぼ)唯一ブラウザ上で動く言語
- 動的なWebサイトで使われる
- Developer Tools で試せる：`F12` or `Ctrl+Shift+I`
    - 実はDiscordでも開ける

## JavaScriptの特徴
- 数値
    - `1 + 1`
    - `10 - 5`
    - `2 * 3`
    - `4 / 2`
- 文字
    - `'Java' + 'Script'`
- 変数と関数
    - 定義と代入
        - `variable = 10`
    - var
        - 古い仕様
        - 使えるけど非推奨
    - let
        - 基本的にvarと同じ
        - 再代入できる
    - const
        - 変数定義時にしか代入できない
        - 再代入しようとするとエラー
- 配列(Array)とオブジェクト(Object)
    - `[1,2,3,4,5]`
    - `{'test': 1, 'test2': 2}`
- 特殊な型
    - true
        - `Boolean(0);`
    - false
        - `Boolean([]);`
    - null
    - undefined
    - Infinity
        - `1/0`
        - `-1/0`
    - [NaN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/NaN)
        - `0 * Infinity`
        - `'JavaScript' * 3`
- 比較演算子
    - 等価演算子/不等価演算子 `==` `!=`
        - `1 == '1'`
        - `null == undefined`
    - 厳密等価演算子/厳密不等価演算子 `===` `!==`
        - `1 === '1'`
        - `null === undefined`
- ブラウザ向けの関数
    - `alert('ここにメッセージを自由に書いてね')`

## [Node.js](https://nodejs.org/ja/)
- PC(サーバー)上でJavaScriptを動かせる環境
- `$ node` でインタプリタ起動
    - `.exit` で終了
- ライブラリ管理ツール npm
    - Node package manager

## [discord.js](https://discord.js.org/#/)
- $ git clone https://github.com/DiscordBotPortalJP/discordjs-startup.git
    - [discordjs-startup](https://github.com/DiscordBotPortalJP/discordjs-startup)
- `$ npm install`