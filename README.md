# 不動産 AI エージェント

商業施設PM向けの静的Webデモです。`index.html` 単体で動作し、GitHub Pages でそのまま公開できます。

## 同梱ファイル

- `index.html` : アプリ本体
- `.nojekyll` : GitHub Pages の Jekyll 処理を無効化
- `.github/workflows/deploy-pages.yml` : GitHub Actions で自動公開する設定
- `README.md` : 公開手順

## ローカル確認

### そのまま開く

```bash
open index.html
```

### 簡易サーバーで開く

```bash
python3 -m http.server 8000
```

ブラウザで `http://localhost:8000` を開いて確認してください。

---

## GitHub Pages 公開手順

GitHub Pages は大きく2通りあります。

- **最短で公開したい** → ブランチ公開
- **更新のたびに自動デプロイしたい** → GitHub Actions 公開

このリポジトリには両方対応できるようにしてあります。

---

## 方法A: いちばん簡単な公開方法（Deploy from a branch）

1. GitHub で新しいリポジトリを作成します。
2. このフォルダの中身をそのままアップロードします。
3. GitHub の対象リポジトリで **Settings** → **Pages** を開きます。
4. **Build and deployment** の **Source** で **Deploy from a branch** を選びます。
5. **Branch** で `main`、フォルダは `/ (root)` を選びます。
6. 保存後、数分で公開されます。

公開URLの例:

```text
https://<GitHubユーザー名>.github.io/<リポジトリ名>/
```

### この方法で使うファイル

- `index.html`
- `.nojekyll`
- `README.md`

`.github/workflows/deploy-pages.yml` は残していても問題ありませんが、使わないなら削除しても構いません。

---

## 方法B: 自動公開する方法（GitHub Actions）

このフォルダには GitHub Pages 用の workflow が入っています。
`main` に push すると自動で Pages にデプロイされます。

### 手順

1. GitHub で新しいリポジトリを作成します。
2. このフォルダの中身をそのまま push します。
3. GitHub の対象リポジトリで **Settings** → **Pages** を開きます。
4. **Build and deployment** の **Source** で **GitHub Actions** を選びます。
5. `main` に push すると自動公開されます。

### 例: Git コマンド

```bash
git init
git add .
git commit -m "Prepare app for GitHub Pages"
git branch -M main
git remote add origin https://github.com/<GitHubユーザー名>/<リポジトリ名>.git
git push -u origin main
```

---

## 公開後に確認すること

- 画像が表示されるか
- デモモードが動くか
- 画面遷移時にエラーが出ないか
- モバイル幅でもレイアウト崩れが大きくないか

---

## 更新方法

### ブランチ公開の場合

`index.html` を更新して `main` に push すると再公開されます。

### GitHub Actions の場合

`main` に push するだけで workflow が走って再公開されます。

---

## 注意点

- このアプリは外部CDNと外部画像を利用しています。
- ネットワーク制限が強い環境では一部表示が遅いことがあります。
- GitHub Pages は静的ホスティングなので、サーバーサイド処理は使っていません。

---

## 推奨運用

実務上は **GitHub Actions 方式** を推奨します。
理由は、更新のたびに公開手順を意識せずに済み、運用事故が少ないためです。
