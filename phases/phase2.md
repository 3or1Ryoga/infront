## PHASE 2-A: src/data/site.ts の作成

全ページから参照するサイト定数を一元管理するファイル。

export const SITE = {
  name:    '株式会社インフロント興産',
  nameEn:  'INFRONT KOSAN Co., Ltd.',
  tel:     '00-0000-0000',
  telHref: 'tel:00-0000-0000',
  email:   'info@infront-kosan.co.jp',
  address: '〒000-0000 ○○県○○市○○',
  copyright: '©2025 INFRONT KOSAN Co.,Ltd.',
} as const;

## PHASE 2-B: src/data/products.json の作成

【重要】このファイルは後でクライアント提供のExcel/CSVから
自動生成されたデータに丸ごと置き換わる。
スキーマを厳守すること。

カテゴリ3種×合計12点のダミーデータを作成:
- "研削材料"     → 5点
- "セラミックス原材料" → 4点
- "工業用副資材" → 3点

1製品あたりのスキーマ（厳守）:
{
  "id":          "TBA-001",           // ユニークID。アンカーリンクに使用
  "name":        "褐色電融アルミナ研磨材",  // 製品名
  "code":        "TBA",               // 品番
  "category":    "研削材料",           // 必ず上記3種のいずれか
  "description": "製品説明文（2〜3文）",
  "specs": {
    "granularity":  "F16〜F220",       // 粒度。ない製品は null
    "bulk_density": "1.85",            // 嵩比重。ない製品は null
    "analysis": [                      // 分析値（製品ごとに項目数が異なってよい）
      { "label": "Al₂O₃", "value": "94.5％" },
      { "label": "SiO₂",  "value": "1.96％" },
      { "label": "TiO₂",  "value": "2.36％" },
      { "label": "Fe₂O₃", "value": "0.35％" }
    ],
    "notes": null    // 補足テキスト。不要なら null
  },
  "image": "/images/products/placeholder.jpg"
}

化学式の組み合わせは製品ごとに変えてリアリティを出すこと。
使用する化学式例: Al₂O₃, SiO₂, TiO₂, Fe₂O₃, MgO, CaO, Na₂O, SiC, Cr₂O₃, V₂O₅


## PHASE 2-C: コンポーネント作成

### src/layouts/Layout.astro
- Props: { title: string; description: string }
- <html lang="ja">
- <head>: charset, viewport, title, description, OGP基本タグ, Google Fonts（preconnect付き）
- <body>: <Header /> → <slot /> → <Footer />

---

### src/components/Header.astro
大朋興産のヘッダーを踏襲:
- 白背景・固定（sticky top-0 z-50）
- 左: テキストロゴ「株式会社インフロント興産」（font-serif、クリックで /）
- 右: ナビリンク「TOP / 会社概要 / 製品一覧」
- 右端: 「お問い合わせ」ボタン（<a href="mailto:...">、SlantButtonコンポーネント使用）
- スクロール量が50pxを超えたら shadow-md を追加（<script>タグで実装）
- モバイル（md未満）: ハンバーガーメニュー。Tailwind onlyでレイアウト、
  開閉JSは<script>タグに含める

---

### src/components/Footer.astro
大朋興産のフッターを踏襲:
- dark背景（#1A1A1A）・白テキスト
- 上段: 左=社名+ナビリンク（縦並び）、右=TEL+mailto リンク
- 下段: SITE.copyright を中央配置
- 全テキストはSITE定数から参照

---

### src/components/SlantButton.astro
【最重要】大朋興産のCTAボタンを完全再現。

Props:
- text:      string  （ボタンテキスト）
- href:      string  （リンク先）
- external?: boolean （デフォルトfalse。trueでtarget="_blank" rel="noopener"）

実装仕様:
- <a> タグで実装（buttonタグ禁止）
- clip-path: polygon() を使い、左80%=朱色/右20%=墨色に斜めに分割
  linear-gradient は使わないこと（印刷時や一部ブラウザで崩れるため）
  clip-pathの具体的なpolygon値は自分でベストな値を判断して設定すること
- ホバー時: 全体を #1A1A1A に変える（transition: background-color 0.3s ease）
  ※clip-pathのアニメは複雑なのでbackground-colorの切り替えで対応する
- テキスト: 白・中央配置・font-semibold・z-index を確保
- サイズ: px-8 py-3、min-w-[200px]
- インラインstyleは使わず、Tailwindクラスで実装

---

### src/components/SectionLabel.astro
各セクション冒頭の英語+日本語ラベルを共通化:
- Props: { en: string; ja: string }
- en: 英語ラベル（text-sm・tracking-widest・text-primary・uppercase）
- ja: 日本語見出し（font-serif・text-3xl md:text-4xl・mt-2）