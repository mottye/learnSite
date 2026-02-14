# LearnSite — 学ぶためのブログ

SmartScope 風の「学ぶブログ」を MkDocs + Material テーマで構築するプロジェクトです。

## クイックスタート

### 1. 依存関係のインストール

**仮想環境を使う場合（推奨）**

```bash
cd /Users/mottye/work/learnSite
python3 -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

**仮想環境を使わない場合**

```bash
cd /Users/mottye/work/learnSite
pip install -r requirements.txt
```

### 2. 開発サーバーでプレビュー

```bash
# 仮想環境を使っている場合
source .venv/bin/activate
mkdocs serve

# または venv 内の mkdocs を直接実行
.venv/bin/mkdocs serve
```

ブラウザで **http://127.0.0.1:8000** を開くとサイトが表示されます。  
`docs/` 内の Markdown を編集すると、自動でリロードされます。

### 3. 静的サイトのビルド（公開用）

```bash
mkdocs build
```

生成されたファイルは `site/` に出力されます。GitHub Pages や Netlify などにデプロイして公開できます。

### 4. GitHub Pages で公開（GitHub Actions）

このリポジトリには **GitHub Actions で MkDocs をビルドし、GitHub Pages にデプロイする** ワークフローが含まれています。

1. **リポジトリを GitHub に push**  
   `main` ブランチに push すると、自動でビルド＆デプロイが走ります。

2. **Pages の有効化（初回のみ）**  
   - リポジトリの **Settings** → **Pages**  
   - **Source** で **GitHub Actions** を選択  

3. **`mkdocs.yml` の URL を自分のリポジトリに合わせる**  
   ```yaml
   site_url: https://<あなたのユーザー名>.github.io/learnSite/
   repo_url: https://github.com/<あなたのユーザー名>/learnSite
   ```

これで `https://<ユーザー名>.github.io/learnSite/` でサイトが公開されます。手動で実行したい場合は Actions タブから「Deploy to GitHub Pages」ワークフローを **Run workflow** で実行できます。

## ディレクトリ構成

```
learnSite/
├── .github/workflows/
│   └── deploy.yml   # GitHub Actions（ビルド＆GitHub Pages デプロイ）
├── mkdocs.yml       # 設定（サイト名・ナビ・テーマ・プラグイン）
├── requirements.txt # Python 依存関係
├── README.md
└── docs/            # コンテンツ（Markdown）
    ├── index.md     # ホーム
    ├── guides/      # スタートガイド
    ├── blog/        # ブログ記事
    ├── tags.md      # タグ一覧
    └── about.md     # このサイトについて
```

## 記事の追加方法

1. `docs/blog/` に新しい `.md` ファイルを作成（例: `my-post.md`）
2. `mkdocs.yml` の `nav` の「ブログ」セクションに追加:
   ```yaml
   - ブログ:
       - 一覧: blog/index.md
       - はじめに: blog/getting-started.md
       - マイ記事: blog/my-post.md
   ```
3. 必要に応じて `docs/blog/index.md` の記事一覧テーブルにも追加

## 参考

- [MkDocs 公式](https://www.mkdocs.org/)
- [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)
- 構成の参考: [SmartScope](https://smartscope.blog/)
