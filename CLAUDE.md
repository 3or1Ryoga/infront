# インフロント興産 Webサイト プロジェクト仕様

## 技術スタック
- Framework: Astro（静的出力）
- Styling: Tailwind CSS v4
- Language: TypeScript（Relaxed）
- Deploy: Vercel

## サイト構成
- /          : トップページ（src/pages/index.astro）
- /company   : 会社概要（src/pages/company.astro）
- /products  : 製品一覧（src/pages/products.astro）

## 重要ルール
- サイト定数は src/data/site.ts の SITE オブジェクトから参照すること
- 製品データは src/data/products.json から読み込むこと
- お問い合わせはフォームなし。tel/mailtoリンクのみ
- 製品カードは必ず .map() でループ生成すること（手書き禁止）
- インラインstyleは使わず Tailwind クラスで実装すること
- clip-path を使う箇所では linear-gradient を使わないこと

## デザイン
- 参考サイト: https://www.taiho-kosan.co.jp/（構成・雰囲気を最大限踏襲）
- primary:   #B22222（朱色）
- dark:      #1A1A1A（墨色）
- off-white: #F5F5F0
- 見出しフォント: Noto Serif JP
- 本文フォント:   Noto Sans JP