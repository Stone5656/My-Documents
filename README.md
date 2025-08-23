# My-Documents

Obsidian（ローカル）で書いたノートのうち、`public/` フォルダを公開するための MkDocs プロジェクトです。  
**標準の自動ナビゲーション**で運用しています。

<p align="center">
  <a href="https://stone5656.github.io/My-Documents/">🌐 GitHub Pages 公開サイトはこちら</a>
</p>

<p align="center">
  <a href="https://github.com/Stone5656/IMy-Documents/main/LICENSE">
    <img src="https://img.shields.io/badge/License-MIT-informational?style=for-the-badge" alt="License: MIT">
  </a>
</p>

> リポジトリ: https://github.com/Stone5656/IMy-Documents

---

## ディレクトリ構成

```

/data/Obsidian/                # プロジェクトルート（mkdocs.yml あり）
├─ docs/                       # ← 公開用。ここを MkDocs が参照
│  ├─ index.md
│  └─ howto/
│     └─ git.md
└─ vault/                      # Obsidian Vault
├─ public/                  # ← 公開対象（ここから docs/ に同期）
└─ private/                 # ← 非公開

```

## 前提
- Arch Linux 推奨パッケージ：`mkdocs`, `mkdocs-material`

```bash
sudo pacman -S mkdocs mkdocs-material
```

> Actions（CI）でのビルドは、ランナーに MkDocs が無いと失敗します。
> いまは **ローカルでビルド/デプロイ** する運用にしています。

## 基本フロー

1. Obsidian で `vault/public/` にノートを作成・更新

2. 同期（**完全同期。削除注意**）

   ```bash
   rsync -av --delete /data/Obsidian/vault/public/ /data/Obsidian/docs/
   ```

   * 事前確認（ドライラン）:

     ```bash
     rsync -aniv --delete /data/Obsidian/vault/public/ /data/Obsidian/docs/
     ```

3. ローカルプレビュー

   ```bash
   mkdocs serve
   ```

4. 本番生成

   ```bash
   mkdocs build --clean
   ```

5. GitHub Pages へデプロイ（ローカルから）

   ```bash
   mkdocs gh-deploy --force
   ```

   * リポジトリ設定の **Settings → Pages** で、Source を `gh-pages` に設定

## ナビゲーションについて

* `mkdocs.yml` で `nav:` を書いていないため、**`docs/` の構造から自動生成**されます。
* 並び順はファイル名のアルファベット順。各ディレクトリの `index.md` は先頭になります。
* 並び順や表示名を細かく制御したくなったら、将来的にプラグイン（例：awesome-pages）を導入してください。

## スクリプト（任意）

* 同期＋ビルド＋プレビュー＋確認して push までを流すスクリプトを `script/` に置いて運用できます。
* `rsync` の `--delete` は強力です。**ドライランでの確認**を推奨します。
