---
description: MkDocs と Material で使える機能一覧。ナビ・プラグイン・Markdown・カスタムの例をまとめています。
---

# MkDocs の機能をフル活用する

このページでは、MkDocs と Material テーマで使える主な機能をまとめています。すでに有効なものと、追加すると便利なものを分けて記載しています。

---

## すでに使っている機能

| 種類 | 内容 |
|------|------|
| **テーマ** | Material、日本語、ライト/ダーク切り替え |
| **ナビ** | タブ・セクション・折りたたみ・トップへ、インスタント遷移 |
| **検索** | サイト内検索（サジェスト・ハイライト）、日本語対応 |
| **コンテンツ** | コードコピー、タブ付きコンテンツ |
| **Markdown** | アドモニション、脚注、タブ、コードハイライト、TOC アンカーリンク |

---

## テーマで追加できる機能（theme.features）

`mkdocs.yml` の `theme.features` に次のいずれかを追加できます。

| 機能 | 説明 |
|------|------|
| `navigation.footer` | フッターに「前のページ」「次のページ」リンクを表示 |
| `navigation.path` | ページ上部にパンくずリスト（例: ホーム > ブログ > 記事名） |
| `toc.follow` | サイドバーの目次がスクロールに追従 |
| `content.action.edit` | 「このページを編集」ボタンを表示（`edit_uri` と連動） |
| `content.action.view` | 「ソースを表示」ボタン（GitHub の raw など） |

---

## Material の組み込みプラグイン

`plugins:` に追加するだけで使えます。

| プラグイン | 説明 | 備考 |
|------------|------|------|
| **tags** | ページにタグを付けて一覧・フィルタ | front matter で `tags: [タグ1, タグ2]`、タグ一覧ページが自動生成される |
| **social** | 各ページ用の OGP 画像（SNS カード）を自動生成 | 日本語は `font_family: Noto Sans JP` 推奨。**画像処理用の依存**（cairosvg 等）が必要 |
| **optimize** | 画像の圧縮・最適化 | 画像が多いとビルドが軽く・速くなる。**画像処理の依存**が必要 |
| **meta** | フォルダ単位で front matter をまとめて管理 | `docs/blog/.meta.yml` でブログ全体に `description` などを一括設定 |
| **blog** | ブログ機能（日付・一覧・アーカイブ） | 導入すると `blog/` の構成がプラグイン仕様になる。既存の手動ブログと併用するか検討 |
| **privacy** | 外部アセットを自ホスト（GDPR 向け） | フォントやスクリプトをローカルに取り込む |
| **offline** | オフライン閲覧用（PWA 風） | サイトを zip で配布するような用途向け |

---

## Markdown 拡張で追加できる表現

`markdown_extensions:` に追加できます。

| 拡張 | 用途 | 例 |
|------|------|-----|
| `pymdownx.emoji` | 絵文字 | `:smile:` → 😊 |
| `pymdownx.keys` | キーボード表記 | `++ctrl+c++` → Ctrl+C 風表示 |
| `pymdownx.tasklist` | タスクリスト（チェックボックス） | `- [ ] TODO` / `- [x] 完了` |
| `pymdownx.arithmatex` | 数式（LaTeX） | `$E = mc^2$`（要 JavaScript または build 時レンダリング） |
| `tables` | テーブル（標準的には既に有効） | 表組み |

---

## フッター・SNS リンク（extra）

`mkdocs.yml` の `extra:` で設定できます。

```yaml
# フッターの SNS リンク
extra:
  social:
    - icon: fontawesome/brands/github
      link: https://github.com/mottye
    - icon: fontawesome/brands/x-twitter
      link: https://twitter.com/your_id
```

アイコンは [Material のアイコン一覧](https://squidfunk.github.io/mkdocs-material/reference/icons-emojis/) で検索できます。

---

## ページごとのメタデータ（front matter）

各 `.md` の先頭で使える主な項目です。

| プロパティ | 説明 |
|------------|------|
| `title` | ブラウザタブ・OGP のタイトル（省略時は見出しから自動） |
| `description` | メタ説明・OGP の説明（160 字以内推奨） |
| `icon` | ナビに表示するアイコン（例: `material/book`） |
| `status` | ステータス表示（`new` / `deprecated` など。`extra.status` で文言を定義） |
| `hide` | 非表示にする要素（例: `footer` で前後リンクを非表示） |

---

## アドモニションの種類（すでに利用可能）

```markdown
!!! note "メモ"
!!! tip "ヒント"
!!! warning "注意"
!!! danger "危険"
!!! info "情報"
!!! success "成功"
!!! bug "バグ"
!!! example "例"
!!! quote "引用"
```

---

## カスタム（上級）

- **テーマの拡張**: `overrides/` に HTML を置いてブロックを上書き（ロゴ・フッター・`extrahead` など）。
- **独自 CSS/JS**: `docs/stylesheets/` と `docs/javascripts/` にファイルを置き、`extra_css` / `extra_javascript` で読み込む。
- **robots メタ**: テーマ拡張で `extrahead` に `<meta name="robots" content="...">` を追加可能。

詳細は [Material for MkDocs 公式](https://squidfunk.github.io/mkdocs-material/) を参照してください。
