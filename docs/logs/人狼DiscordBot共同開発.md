https://twitter.com/discordbot_jp/status/1256238250886418433
https://twitter.com/discordbot_jp/status/1256576976942333953

# 準備が必要なもの

- Discord Bot アカウント
- Python と discord.py のインストール
- コードエディタ（VSCodeなど）

# 1日目： 開発開始から機能追加まで

## 講義内容

- 新規開発の考え方
- Discord Bot 新規開発のセットアップ
    - [DiscordBotPortalJP/discordpy-startup: discord.py on Heroku](https://github.com/DiscordBotPortalJP/discordpy-startup)
- discord.py の基本
- Git と GitHub の概要
- 新規開発のゴールを決める
- ざっくりと全体的な仕様とタスクを書き出す
- プロトタイピング
    - [ゲームのステータスを管理するコマンド群を追加 by 1ntegrale9 · Pull Request #1 · DiscordBotPortalJP/werewolf](https://github.com/DiscordBotPortalJP/werewolf/pull/1)

## 新規開発で大事なこと

- 限られた時間(GWの5日間)で完成させられるか？
- やりたいことはたくさんあるけれど、小さいゴールを決めることが大事

## 人狼ゲーム（汝は人狼なりや？） について

### 基本的な流れの確認

- 村人陣営と人狼陣営に分かれる
- 昼と夜のターン制で処刑と襲撃を繰り返す
- 人狼が全員死亡したら村人陣営が勝利
- 村人の数が人狼の数以下になったら人狼陣営が勝利

### ざっくりとした仕様

- データ
    - GM：bot
    - 参加者
    - 村人陣営： 村人、占い師、霊能者（霊媒師）、狩人（騎士）
    - 人狼陣営： 人狼
    - 妖狐(狐)陣営： 妖狐(狐)
    - 編成テンプレート
        - 4:村村占狼
        - 5:村村村占狼
    - ターン制
        - 日数
        - 昼、夜
- 機能
    - 参加者の募集
    - プレイヤー参加
    - ゲーム開始
    - 役職の割り振り
    - 投票セット
    - 占いセット
    - 襲撃セット
    - 処刑処理
    - 襲撃処理
    - ゲーム終了判定
        - ゲーム結果の表示
    - 日付変更処理
        - 占い判定処理
        - 襲撃結果(生存状況)表示
            - 「Aさんが無残な姿で発見されました」
        - 占い結果表示

### 上記のうち新規開発では扱わない仕様

- 村人陣営：霊能者（霊媒師）、狩人（騎士）
- 人狼陣営：狂人
- 妖狐(狐)陣営：妖狐(狐)
- ターン制：昼、夜

# 2日目： Git/GitHub を利用した開発フロー

## 講習内容

[ゲーム開始までに必要なコードの雛形を作成 by 1ntegrale9 · Pull Request #4 · DiscordBotPortalJP/werewolf](https://github.com/DiscordBotPortalJP/werewolf/pull/4)

- GitHubとは何か？
- Issue と Pull Request について
- GitHub Actions による構文チェックの自動化

## 進めるタスクと仕様の決定

- 参加者募集
    - ゲームステータスの定義（終わってる）
    - 募集コマンドの実装（終わってる）
- プレイヤーの参加
    - 参加者データの管理
    - 参加コマンドの実装
- ゲーム開始
    - 編成テンプレートの定義
    - 参加者に役職を割り振る

# 3日目： 共同開発の進め方

## 講習内容

- GitHub Wiki の使い方
- Pull Request の進め方（コードレビュー、Merge）
- VSCode Live Share によるリモートペアプログラミング

[Messages · DiscordBotPortalJP/werewolf Wiki](https://github.com/DiscordBotPortalJP/werewolf/wiki/Messages)
[[Add] joinコマンドの実装 by daima3629 · Pull Request #5 · DiscordBotPortalJP/werewolf](https://github.com/DiscordBotPortalJP/werewolf/pull/5)
[[Add]startコマンドを実装 by disneyresidents · Pull Request #6 · DiscordBotPortalJP/werewolf](https://github.com/DiscordBotPortalJP/werewolf/pull/6)

## 進めるタスクと仕様の決定

- 投票セット
    - Playerクラスに投票先プロパティを生やす（初期値None)
    - 投票コマンドで投票先のPlayerをセット
- 占いセット
    - Playerクラスに占い先プロパティを生やす（初期値None)
    - 占いコマンドで占い先のPlayerをセット
- 襲撃セット
    - Playerクラスに襲撃先プロパティを生やす（初期値None)
    - 襲撃コマンドで襲撃先のPlayerをセット
- 日付変更処理
    - 投票、占い、襲撃セット時に全員のセット先をチェックして全員 not None なら実行
    - 処刑処理
        - Playerに生存(死亡)フラグを持たせる
        - 投票先を集計して1番票が多い人を処刑
        - 票トップが複数名いる場合はランダムで処刑
    - 襲撃処理
        - Playerに生存(死亡)フラグを持たせる
        - 襲撃先を集計して1番票が多い人を襲撃
        - 票トップが複数名いる場合はランダムで襲撃
        - 既に処刑されている場合はスキップ
    - ゲーム終了判定
        - 人狼の数 == 0 で村人陣営の勝利判定
        - 村人の数 <= 人狼の数 で人狼陣営の勝利判定
        - ゲーム結果の表示
    - 占い判定処理
        - 占い先が村人扱いか人狼扱いかを判定
        - 占い師にDMで結果を送信
    - 生存状況（処刑結果、襲撃結果）表示
        - 「投票の結果Aさんが処刑されました」
        - 「Bさんが無残な姿で発見されました」
    - 投票、占い、襲撃先をリセット(Noneをセット)

# 4日目： 開発速度、品質、設計、テスト

- 最初に頭に入れておくと良い設計用語
    - 驚き最小の原則
    - 関心の分離
    - 単一責任原則
    - DRY: Don't repeat yourself
    - KISS: Keep It Simple, Stupid
    - YAGNI: You ain't gonna need it
    - デザインパターン（GoF）
    - ドメイン駆動設計
        - ドメインモデリング
        - ユビキタス言語
- [プログラマが知るべき97のこと](https://xn--97-273ae6a4irb6e2hsoiozc2g4b8082p.com/)

# 5日目： OSSとして公開する

- README.md について
- pip install できるようにするには
