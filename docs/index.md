# My Knowledge Base

ようこそ。ここは Obsidian の `public/` を同期して公開しているナレッジベースです。  
ナビゲーションは **ディレクトリ構造から自動生成**（`nav` 未指定）されます。  
> そのため、ページの並び順は “ファイル名のアルファベット順 / 各階層の `index.md` が先頭” になります。

## はじめに
- このサイトは [MkDocs + Material テーマ] で生成されています。
- 公開したいノートは **`vault/public/`** に置き、`docs/` に同期してからビルドします。
- 非公開ノートは `vault/private/` に置いてください（公開対象外）。
## 運用メモ
- 同期: `rsync -av --delete /data/Obsidian/vault/public/ /data/Obsidian/docs/`
- プレビュー: `mkdocs serve`
- ビルド: `mkdocs build --clean`
- 公開（ローカルから）: `mkdocs gh-deploy --force`

