# WebAPI&HTTP基礎編

## DiscordBot が使っている DiscordAPI の話
- https://discord.com/developers
    - discord.com -> ヘルプ -> デベロッパー向け
- discord.py や discord.js が DiscordAPI を使っています

## APIとHTTPの概要の解説（10分）
- WebAPIとは
    - Web上のHTTPに準拠したAPI
- APIとは
    - Application Programming Interface
- HTTPとは
    - Hypertext Transfer Protocol の略
    - [HTTP リクエストメソッド](https://developer.mozilla.org/ja/docs/Web/HTTP/Methods)
        - GET: データを取ってきてほしい時に使う
        - POST / PUT: データを送る時に使う
        - DELETE: データを削除してほしい時に使う
    - [HTTP レスポンスステータスコード](https://developer.mozilla.org/ja/docs/Web/HTTP/Status)
        - 実行した結果がどうなったかを教えてくれる
        - 数字に意味付けられている
            - 403: 権限が無い時
            - 404: 存在しない時
        - GET したら基本は 200 が返ってくる
    - [HTTP ヘッダー](https://developer.mozilla.org/ja/docs/Web/HTTP/Headers)
        - 込み入った話なので今回は割愛

## PythonとJavaScriptを使って色んなAPIを使ってみる（15分）
- Pythonの場合
    - [Requests](https://requests-docs-ja.readthedocs.io/en/latest/)(同期)
    - [AIOHTTP](https://docs.aiohttp.org/en/stable/)(非同期)
- JavaScriptの場合
    - [axios](https://www.npmjs.com/package/axios)

### requests を使って API を使ってみる

`pip install requests` をしておく

```python
import requests
from pprint import pprint

URL_API = 'https://qiita.com/api/v2'

res = requests.get(f'{URL_API}/tags')
pprint(res.json())
```

### aiohttp を使って API を使ってみる

```python
from discord import Intents
from discord.ext import commands
import os
import aiohttp

bot = commands.Bot(
    command_prefix=commands.when_mentioned_or('/'),
    help_command=None,
    intents=Intents.all(),
)
token = os.environ['DISCORD_BOT_TOKEN']


@bot.command()
async def test(ctx):
    async with aiohttp.ClientSession() as session:
        async with session.get('https://qiita.com/api/v2/tags') as res:
            tags = await res.json()
            await ctx.send(tags)

bot.run(token)
```

## 実際にAPIを作って使ってみる（15分）

- [FastAPI](https://fastapi.tiangolo.com/)
- [1ntegrale9/fastapi-heroku-template](https://github.com/1ntegrale9/fastapi-heroku-template)

### 作る時

- Web フレームワークを使うと楽
- Python だと FastAPI が一応流行ってるらしい(他には Flask, Django REST Framework とかがある)
- JS は Express.js

### FastAPI 解説

1. コード

```python
from fastapi import FastAPI

# アプリケーションの初期化
app = FastAPI(
    title='FastAPI Heroku Template',
    description='HerokuでFastAPIによるWebAPIを作成するためのテンプレート',
    docs_url='/'
)

# /api/ に GET リクエストが送られた時の処理
@app.get('/api')
def get_sample() -> str:
    return 'sample' # 返したいデータを return する

# /api/post/ に POST リクエストが送られた時の処理
@app.post('/api/post')
def post_sample(sample: str): # 送ってほしいデータを引数に入れる
    # 変数名が JSON のキー, アノテーションされている型が欲しいデータの型
    return sample
```

- API の仕様書を自動で作ってくれる

2. uvicorn を使うと、いい感じに動かしてくれる
- [uvicorn](https://www.uvicorn.org/)
  - Python のサーバーフレームワーク
  - 非同期処理に対応
