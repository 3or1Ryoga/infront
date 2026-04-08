# infront-kosan-web

株式会社インフロント興産 コーポレートサイト

## セットアップ

```bash
npm install
npm run dev     # http://localhost:4321
```

## コマンド

```bash
npm run dev      # 開発サーバー起動
npm run build    # 本番ビルド（エラー0を確認すること）
npm run preview  # ビルド結果を確認
```

## 技術スタック

- Astro 6 + Tailwind CSS v4
- TypeScript（Relaxed）
- デプロイ: Vercel（git push で自動デプロイ）

## ディレクトリ構成

```
src/
├── components/
│   ├── Header.astro       # ロゴ・ナビ・モバイルメニュー（スクロールshadow付き）
│   ├── Footer.astro       # 社名・ナビ・TEL/メール・コピーライト
│   ├── SlantButton.astro  # clip-path で斜め分割したCTAボタン
│   └── SectionLabel.astro # en/ja セクション見出しラベル
├── data/
│   ├── site.ts            # 会社情報定数（SITE）
│   └── products.json      # 製品データ 12点・3カテゴリ
├── layouts/
│   └── Layout.astro       # <head>・OGP・Google Fonts・Header/Footer
├── pages/
│   ├── index.astro        # トップページ（5セクション）
│   ├── company.astro      # 会社概要ページ
│   └── products.astro     # 製品一覧ページ
└── styles/
    └── global.css         # Tailwindテーマ定義・ベーススタイル
public/
└── images/
    └── products/
        └── placeholder.jpg  # 製品画像プレースホルダー
phases/                      # Claude Code 用フェーズ別指示書
```

## サイト構成

| パス        | ページ   | 概要                                        |
|-------------|---------|---------------------------------------------|
| `/`         | トップ   | Hero / About / Products / Sustainability / CTA |
| `/company`  | 会社概要 | 会社情報テーブル / アクセスマップ / CTA        |
| `/products` | 製品一覧 | カテゴリナビ / 製品カード（スペック詳細）/ CTA |

## デザイン仕様

| 項目       | 値                        |
|-----------|--------------------------|
| primary   | `#B22222`（朱色）          |
| dark      | `#1A1A1A`（墨色）          |
| off-white | `#F5F5F0`（セクション背景） |
| light     | `#FFFFFF`（ベース背景）     |
| 見出し     | Noto Serif JP             |
| 本文       | Noto Sans JP              |

## コーディングルール

- サイト定数は `src/data/site.ts` の `SITE` から参照する
- 製品データは `src/data/products.json` から読み込む（スキーマ変更禁止）
- リスト描画は必ず `.map()` でループ（手書き禁止）
- Tailwind クラスで実装する（インライン style 禁止）
- `clip-path` を使う箇所で `linear-gradient` を使わない
- お問い合わせは `tel:` / `mailto:` リンクのみ（フォームなし）

## 製品データスキーマ

`products.json` は後でクライアント提供データに丸ごと置き換わる予定。スキーマを厳守すること。

```jsonc
{
  "id":          "GR-001",
  "name":        "褐色電融アルミナ研磨材",
  "code":        "BFA",
  "category":    "研削材料",          // "研削材料" | "セラミックス原材料" | "工業用副資材"
  "description": "製品説明文",
  "specs": {
    "granularity":  "F16〜F220",       // null 可
    "bulk_density": "1.85",            // null 可
    "analysis": [
      { "label": "Al₂O₃", "value": "94.5％" }
    ],
    "notes": null                      // null 可
  },
  "image": "/images/products/placeholder.jpg"
}
```

## 開発フロー

```
フェーズ単位で実装 → npm run build 確認（エラー0）→ git commit → 次のフェーズへ
```

## 実装済みフェーズ

| フェーズ | 内容                                          | コミット  |
|---------|----------------------------------------------|---------|
| Phase 0 | Astro + Tailwind 環境構築・3ページ骨格         | ffe9d8d |
| Phase 1 | Tailwind カスタムテーマ・Google Fonts・グローバルCSS | a36e70e |
| Phase 2 | site.ts / products.json スキーマ確定・SlantButton / SectionLabel コンポーネント | 414d801 |
| Phase 3 | トップページ 5セクション実装                   | 0a84a6f |
| Phase 4 | 会社概要ページ実装（会社情報・アクセスマップ）  | 1b49f69 |
| Phase 5 | 製品一覧ページ実装（カテゴリナビ・製品カード）  | a77e866 |

## 担当

酒井涼雅 / r.sakai@gakusei-engineer.com
