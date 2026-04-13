# 不動産 AI エージェント — 商業施設 PM 向け意思決定レイヤー

> Edutex Co., Ltd. が開発した、テナント中途解約・契約満了・賃料改定の損失局面を  
> 後継誘致・更新・売却の収益機会へ変えるAI意思決定Webアプリです。

![Demo](https://img.shields.io/badge/demo-GitHub%20Pages-blue?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)

---

## 機能一覧

| 画面 | 説明 |
|------|------|
| ダッシュボード | KPI・全国物件マップ・緊急アラート・PoC達成指標 |
| 物件管理 | 130施設をカード表示、タイプ別フィルター |
| アラート | 3段階（緊急/注意/把握）の一覧と詳細モーダル |
| AI エージェント | 案件選択→AI自動分析→チャット形式で提案生成 |
| シナリオ比較 | 後継誘致/更新・更地返還/売却の3案をスコア付き比較 |
| タスク管理 | カンバン形式（未着手/進行中/完了） |
| 効果分析 | ROI試算・月次空室率グラフ・施設タイプ別効果表 |
| **デモモード** | **5件同時解約シナリオをステップ再生** |

---

## GitHub Pages への公開手順

### 方法 A — GitHub Web UI（最短 3 分）

1. **リポジトリを作成**  
   GitHub で `New repository` → 任意の名前（例: `fudosan-ai-agent`）→ **Public** → `Create repository`

2. **ファイルをアップロード**  
   `Add file` → `Upload files` から以下をドラッグ＆ドロップ：
   - `index.html`
   - `.nojekyll`

3. **GitHub Pages を有効化**  
   `Settings` → `Pages` → `Source: Deploy from a branch` → `Branch: main / (root)` → `Save`

4. **公開URLを確認**  
   数分後に `https://<ユーザー名>.github.io/<リポジトリ名>/` でアクセス可能になります。

---

### 方法 B — Git CLI（推奨）

```bash
# 1. このディレクトリで Git 初期化
cd /path/to/myproject2
git init
git add index.html .nojekyll README.md

# 2. 初回コミット
git commit -m "feat: 不動産AIエージェント初回リリース"

# 3. GitHub にリポジトリを作成（gh CLI を使う場合）
gh repo create fudosan-ai-agent --public --source=. --remote=origin --push

# gh CLI がない場合は GitHub でリポジトリ作成後:
# git remote add origin https://github.com/<ユーザー名>/fudosan-ai-agent.git
# git branch -M main
# git push -u origin main

# 4. GitHub Pages を有効化
gh api repos/<ユーザー名>/fudosan-ai-agent/pages \
  --method POST \
  -f build_type=legacy \
  -f source.branch=main \
  -f source.path=/
```

> **確認コマンド**（公開URLが表示されます）
> ```bash
> gh api repos/<ユーザー名>/fudosan-ai-agent/pages --jq '.html_url'
> ```

---

### 方法 C — GitHub Actions（CI/CD）

`.github/workflows/deploy.yml` を作成して自動デプロイ：

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [main]

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  deploy:
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - uses: actions/checkout@v4
      - uses: actions/configure-pages@v5
      - uses: actions/upload-pages-artifact@v3
        with:
          path: .
      - id: deployment
        uses: actions/deploy-pages@v4
```

> `Settings` → `Pages` → `Source: GitHub Actions` に変更してから push してください。

---

## ローカルで動かす

外部依存なしで動作します。`index.html` をブラウザで直接開くだけです。

```bash
# macOS
open index.html

# Windows
start index.html

# Python の簡易サーバー（ポート 8000）
python3 -m http.server 8000
# → http://localhost:8000 でアクセス
```

---

## 外部依存（CDN）

| ライブラリ | 用途 | URL |
|-----------|------|-----|
| Tailwind CSS Play CDN | スタイリング | `https://cdn.tailwindcss.com` |
| Google Fonts (Noto Sans JP) | 日本語フォント | `https://fonts.googleapis.com` |
| Unsplash | 物件イメージ | `https://images.unsplash.com` |
| DiceBear | アバター生成 | `https://api.dicebear.com` |

> すべて無料・公開APIです。オフライン環境で動かす場合は各リソースをローカルに配置してください。

---

## 技術スタック

- **フロントエンド**: Vanilla HTML / CSS / JavaScript（フレームワーク不使用）
- **スタイリング**: Tailwind CSS v3 Play CDN
- **デプロイ**: GitHub Pages（静的ホスティング）
- **バックエンド**: なし（フルクライアントサイド）

---

## ライセンス

MIT License — © 2026 Edutex Co., Ltd.
