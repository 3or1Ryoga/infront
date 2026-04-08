## PHASE 3: src/pages/index.astro

大朋興産のトップページ構成をセクション単位で完全に踏襲すること。

---

### Section 1: Hero（ファーストビュー）
- 高さ: min-h-screen
- 背景: bg-dark（後で背景画像に差し替え予定。現時点は #1A1A1A 単色でOK）
- レイアウト: コンテンツ左寄せ（大朋興産と同じ）
- コンテンツ（上から）:
  1. "About us"（text-primary・text-sm・tracking-widest・uppercase）
  2. h1（font-serif・text-white・text-4xl md:text-6xl・leading-tight）:
     「独自の技術と品質で、
      研磨材料の未来を切り開く」
  3. サブコピー（text-white・opacity-80・mt-6）:
     「国内外の厳選素材を、卓越した品質管理でご提供いたします。」
  4. SlantButton: text="製品一覧を見る" href="/products"（mt-10）

---

### Section 2: About
- 背景: bg-off-white・py-20 px-6 md:px-16
- SectionLabel: en="About us" ja="インフロント興産について"
- 説明文（2段落のダミーテキスト、製造業B2Bとして自然な内容）
- 末尾: SlantButton text="会社概要を見る" href="/company"

---

### Section 3: Products
- 背景: bg-light・py-20 px-6 md:px-16
- SectionLabel: en="Products" ja="取り扱い製品カテゴリ"
- 3列グリッド（grid grid-cols-1 md:grid-cols-3 gap-6）:
  カード1: 番号="01" en="Abrasive Materials"      ja="研削材料・研磨材"    href="/products#abrasive"
  カード2: 番号="02" en="Ceramics Raw Materials"   ja="セラミックス原材料"  href="/products#ceramics"
  カード3: 番号="03" en="Industrial Sub-Materials" ja="工業用副資材"        href="/products#industrial"

  各カードスタイル:
  - border border-gray-200・p-8・transition-colors
  - 番号: font-serif・text-4xl・text-primary
  - en: text-xs・tracking-widest・text-gray-400・mt-1
  - ja: font-serif・text-xl・mt-2・text-dark
  - ホバー: border-primary（transition付き）
  - カード全体が <a> タグで該当アンカーへリンク

---

### Section 4: Sustainability
- 背景: bg-dark・py-20 px-6 md:px-16・text-white
- 中央配置（text-center）
- h2（font-serif・text-white）: 「持続可能な社会の実現に向けて」
- 説明文（text-white・opacity-80・max-w-2xl・mx-auto・mt-6、2〜3文）

---

### Section 5: Contact CTA
- 背景: bg-off-white・py-20 px-6 md:px-16
- 中央配置
- h2（font-serif）: 「お問い合わせはお電話・メールにて承ります」
- 2つのSlantButtonを flex gap-4 flex-col sm:flex-row で横並び:
  1. text="お電話でのお問い合わせ" href={SITE.telHref}
  2. text="メールでのお問い合わせ" href={"mailto:" + SITE.email}