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

### 5. カスタムドメインを使う

独自ドメイン（例: `https://blog.example.com`）で公開する場合:

1. **`mkdocs.yml` の `site_url` をドメインに合わせる**
   ```yaml
   site_url: https://blog.example.com/
   ```

2. **GitHub でドメインを設定**
   - リポジトリの **Settings** → **Pages** → **Custom domain**
   - 使うドメインを入力（例: `blog.example.com`）して **Save**
   - GitHub の案内に従い、DNS で **CNAME** または **A レコード** を設定する

3. **HTTPS を有効にする**  
   Custom domain 保存後、**Enforce HTTPS** にチェックを入れる（推奨）。

これでサイトのリンク・OGP・サイトマップがすべてカスタムドメインで生成されます。

### 6. 表示されないとき（トラブルシューティング）

1. **Actions の結果**  
   **Actions** タブで直近の「Deploy to GitHub Pages」を開き、**build** と **deploy** の両方が成功（緑）か確認する。失敗している場合はそのステップのログでエラーを確認する。

2. **GitHub の URL で開く**  
   ブラウザで **https://mottye.github.io/learnSite/** を開く（リポジトリ名が `learnSite` の場合）。
   - **ここで表示される** → デプロイは成功している。カスタムドメイン側（DNS・キャッシュ・Enforce HTTPS）を確認する。
   - **ここでも表示されない** → デプロイかビルドに問題がある。上記の Actions ログを確認する。

3. **Pages の設定**  
   **Settings** → **Pages** で次を確認する。
   - **Build and deployment** の **Source** が **GitHub Actions** になっている。
   - **Custom domain** に `mottye.com` が入っている（使う場合）。保存後 **Enforce HTTPS** にチェックを入れる。

4. **キャッシュ**  
   ブラウザのシークレットウィンドウや別デバイスで https://mottye.com/ を開いてみる。

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
