# 遠隔の人と遊ぶ：Renderへのデプロイ手順

このアプリを **Render**（無料）に置くと、あなたのPCを消していても、
固定URLで24時間いつでも遠隔のメンバーとワークショップができます。

必要なアカウントは2つ（どちらも無料）：
1. **GitHub** … プログラムを保管する場所（あなたのユーザー名は `daichi-nakamura2`）
2. **Render** … プログラムを動かす場所

姉妹アプリ「勇気のしずくゲーム」と同じ手順です。名前を `9masu-writing` に読み替えるだけ。

---

## ステップ1：GitHubにコードを上げる

### 1-1. 新しいリポジトリ（保管箱）を作る
1. https://github.com/new を開く
2. **Repository name** に `9masu-writing` と入力
3. 公開設定は **Public** のままでOK
4. 「Add a README」などのチェックは **付けない**
5. 緑の「Create repository」を押す

### 1-2. コードをアップロードする（どちらか一方）

#### 方法A：ブラウザでドラッグ＆ドロップ（認証設定なしでOK・おすすめ）
1. 作ったリポジトリ画面の「**uploading an existing file**」リンクを押す
2. `9masu-writing` フォルダの中の **次のファイルだけ** をドラッグして入れる
   （このアプリは画面ファイルを**フォルダ直下に平置き**しています。`public` フォルダは作らないこと）：
   - `server.js`
   - `index.html`
   - `style.css`
   - `app.js`
   - `package.json`
   - `package-lock.json`
   - `render.yaml`
   - `.gitignore`
   - `README.md`
   - `DEPLOY.md`

   ⚠️ **`node_modules` フォルダだけは絶対に含めない**（巨大で不要。Render側で自動で入ります）
3. 下の「**Commit changes**」を押す

#### 方法B：ターミナルでコマンド（Personal Access Token がある人向け）
このフォルダはすでに `git commit` 済みです。ターミナルで下記を実行：

```
cd "/Users/a818011/Desktop/ゲーム開発/感謝脳ゲーム/9masu-writing"
git remote add origin https://github.com/daichi-nakamura2/9masu-writing.git
git branch -M main
git push -u origin main
```

ユーザー名・パスワードを聞かれたら、パスワード欄には
GitHubの **Personal Access Token** を入力します
（GitHub → Settings → Developer settings → Personal access tokens で発行）。

---

## ステップ2：Renderで動かす

### 2-1. Renderにログイン
https://render.com にアクセス（勇気のしずくで作ったアカウントがあればそのままログイン）。
新規なら「Get Started」→ **「GitHub」でサインアップ** が楽です。

### 2-2. アプリを作成する
1. ダッシュボード右上「**New +**」→「**Web Service**」
2. GitHub連携を許可し、`9masu-writing` リポジトリを選ぶ
3. 設定は `render.yaml` から自動で読み込まれます。手入力を求められたら：
   - **Language / Runtime**：Node
   - **Build Command**：`npm install`
   - **Start Command**：`npm start`
   - **Instance Type**：**Free**
4. 一番下の「**Create Web Service**」を押す

数分でビルドが終わり、画面上部に
`https://9masu-writing.onrender.com`（または `-xxxx` 付き）のURLが出ます。
**これが遠隔メンバーに配るURLです。**

---

## ステップ3：みんなでワークショップ
- **ファシリテーター**がURLを開いて「部屋を作成」→ 4文字の部屋コードが出る
- **参加者**は同じURLを開いて「部屋に参加」→ 部屋コードと名前を入力
- ⚠️ **参加はロビー中（記入開始前）だけ**。全員そろってから「記入タイムを始める」を押す
- 声はアプリに含まれないので、**Zoom・LINE通話などをつなぎながら**進めてください

---

## 無料プランの注意点
- 15分間だれもアクセスしないとサーバーが休止します。
  次に開くとき最初の表示に **約1分** かかることがあります。始める少し前に一度開いておくとスムーズ。
- 進行中の部屋データはサーバーのメモリ上にあるため、
  再起動・休止すると進行中の部屋は消えます（遊び直せば新しい部屋が作れます）。

## 更新したくなったら
プログラムを直したあと、GitHubに上げ直す（方法A：再アップロード ／ 方法B：`git push`）と、
Renderが自動で作り直して反映します。
