# インフロント興産 Web サイト

## ビルド・確認コマンド
```bash
npm run dev      # 開発サーバー起動 → http://localhost:4321
npm run build    # 本番ビルド（必ずエラー0を確認すること）
npm run preview  # ビルド結果をローカルで確認
```

## 技術スタック
- Astro（静的出力）・Tailwind CSS v4・TypeScript（Relaxed）

## サイト構成
- `/`         → src/pages/index.astro
- `/company`  → src/pages/company.astro
- `/products` → src/pages/products.astro

## コーディングルール
- サイト定数は `src/data/site.ts` の SITE から参照する
- 製品データは `src/data/products.json` から読み込む
- リスト描画は必ず `.map()` でループする（手書き禁止）
- Tailwind クラスで実装する（インラインstyle禁止）
- clip-path を使う箇所で linear-gradient を使わない
- お問い合わせは `tel:` / `mailto:` リンクのみ（フォームなし）

## デザイン
- 参考: https://www.taiho-kosan.co.jp/（構成・雰囲気を踏襲、コードコピー禁止）
- primary `#B22222` / dark `#1A1A1A` / off-white `#F5F5F0`
- 見出し: Noto Serif JP　本文: Noto Sans JP

## フェーズ管理
実装は phases/ フォルダの指示書に従い、1フェーズずつ進める。
次のフェーズに進む前に `npm run build` でエラー0を確認し、git commit すること。

@phases/phase0.md