あなたはプロのWebエンジニアです。
以下の仕様に従い、株式会社インフロント興産のコーポレートサイトを構築してください。

## 技術スタック（環境構築・npm install済みを前提）
- Framework: Astro（最新安定版）
- Styling: Tailwind CSS v4
- Language: TypeScript（tsconfig は Astro デフォルトのまま）
- 出力: Static（output: 'static'）
- デプロイ先: Vercel または Cloudflare Pages（どちらでも動く前提）

## サイト構成（3ページ）
| パス        | ページ       |
|-------------|------------|
| /           | トップページ |
| /company    | 会社概要     |
| /products   | 製品一覧     |

## 参考サイト
https://www.taiho-kosan.co.jp/
大朋興産株式会社のサイト。レイアウト・セクション構成・雰囲気を最大限踏襲すること。
コードをコピーするのではなく、「同じ見た目・同じ構成」になるよう一から実装すること。

## クライアント情報（仮。後で一括置換できるようにハードコードせずに定数管理すること）
- 社名: 株式会社インフロント興産
- 英語社名: INFRONT KOSAN Co., Ltd.
- 業種: 研磨剤・工業材料の製造・販売（B2B）
- 電話: 00-0000-0000（仮）
- メール: info@infront-kosan.co.jp（仮）
- 住所: 〒000-0000 ○○県○○市○○（仮）

これらの定数は src/data/site.ts にまとめて export し、
全コンポーネントからそこを参照する形にすること。
（例: import { SITE } from '../data/site'）

## お問い合わせ方針
フォームは実装しない。電話（tel:リンク）・メール（mailto:リンク）のみ。