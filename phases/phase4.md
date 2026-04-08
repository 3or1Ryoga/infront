## PHASE 4: src/pages/company.astro

---

### ページヘッダーセクション
- 背景: bg-dark・py-20 px-6 md:px-16
- h1（font-serif・text-white）: 「会社概要」
- サブ: "Company"（text-primary・text-sm・tracking-widest）
- パンくずリスト（text-white・text-sm・opacity-60）: TOP > 会社概要

---

### Section 1: 会社概要テーブル
<dl> タグで実装。各行のスタイル:
- flex flex-col sm:flex-row・py-4・border-b border-gray-100
- <dt>: text-sm・font-semibold・text-gray-500・min-w-[140px]・shrink-0
- <dd>: text-dark・mt-1 sm:mt-0

| dt（項目）  | dd（内容）                             |
|------------|--------------------------------------|
| 商号        | 株式会社インフロント興産               |
| 英語表記    | INFRONT KOSAN Co., Ltd.              |
| 設立        | 2010年（仮）                          |
| 資本金      | 1,000万円（仮）                        |
| 代表者      | 代表取締役 ○○ ○○（仮）               |
| 所在地      | {SITE.address}                       |
| 事業内容    | 研磨材料・工業材料の製造・販売         |
| 電話番号    | <a href={SITE.telHref}>{SITE.tel}</a>|
| メール      | <a href={"mailto:"+SITE.email}>...   |

---

### Section 2: アクセス
- SectionLabel: en="Access" ja="所在地・アクセス"
- Googleマップ（仮置き）:
  <iframe
    src="https://maps.google.com/maps?q=大阪市&output=embed"
    width="100%" height="400"
    style="border:0" loading="lazy"
    title="アクセスマップ"
  ></iframe>
- iframeの下に {SITE.address} をテキスト表示

---

### Section 3: Contact CTA
トップページのSection 5と同じ内容を配置（コンポーネント化してもよい）