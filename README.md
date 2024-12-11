# Simple SQL Formatter

SQLを整形するシンプルなWebアプリケーションです。

## 特徴

- 完全にクライアントサイドで動作
- 外部との通信を一切行わないため、機密性の高いSQLも安心して利用可能
- モダンでシンプルなUI
- レスポンシブデザインでPC・スマートフォンに対応

## 対応SQL

以下のSQLダイアレクトに対応しています：

- MySQL
- PostgreSQL
- SQLite
- BigQuery
- DB2
- Hive
- MariaDB
- N1QL
- PL/SQL
- Redshift
- Spark
- T-SQL

## 機能

- SQLの整形
  - 大文字小文字の統一（キーワードは大文字）
  - インデントの適用
  - 改行の最適化
- 整形後のSQLをワンクリックでクリップボードにコピー
- 整形後のSQLも編集可能

## 技術スタック

- [Svelte](https://svelte.dev/)
- [Vite](https://vitejs.dev/)
- [sql-formatter](https://github.com/sql-formatter-org/sql-formatter)

## PWA対応

- オフラインでも利用可能
- ホーム画面に追加可能

## 開発

```bash
# 依存関係のインストール
npm install

# 開発サーバーの起動
npm run dev

# ビルド
npm run build
```

## ライセンス

MIT License
