## PHASE 5: src/pages/products.astro

大朋興産の製品一覧ページのレイアウトを完全に踏襲すること。
products.json を全件読み込み、category でグルーピングして表示する。

---

### 読み込み処理（フロントマター）
import productsData from '../data/products.json';
const categories = [
  { id: 'abrasive',   label: '01 研削材料・研磨材',    value: '研削材料'      },
  { id: 'ceramics',   label: '02 セラミックス原材料',   value: 'セラミックス原材料' },
  { id: 'industrial', label: '03 工業用副資材',         value: '工業用副資材'  },
];

---

### ページヘッダーセクション
- 背景: bg-dark・py-20
- h1（font-serif・text-white）: 「製品一覧」
- サブ: "Products"（text-primary・text-sm・tracking-widest）
- パンくずリスト: TOP > 製品一覧

---

### カテゴリアンカーナビ
大朋興産のタブ型ナビを踏襲:
- 背景: bg-off-white（sticky または固定はしない）
- flex・overflow-x-auto・gap-0・border-b border-gray-200
- categories.map() でリンクを生成:
  <a href="#{id}" class="...">
    {label}
  </a>
- ホバー時: border-b-2 border-primary・text-primary

---

### 製品リスト
categories.map() で各カテゴリのセクションを生成:

<section id={category.id} class="py-16 px-6 md:px-16">
  <h2 class="font-serif text-2xl border-b-2 border-primary pb-3 mb-10">
    {category.label}
  </h2>

  {productsData
    .filter(p => p.category === category.value)
    .map(product => (
      <!-- 製品カード -->
    ))
  }
</section>

---

### 製品カード（1製品あたり）
大朋興産の製品詳細レイアウトを完全再現:

<article class="flex flex-col md:flex-row gap-8 py-12 border-b border-gray-200">

  <!-- 左: 画像エリア -->
  <div class="md:w-[280px] md:shrink-0">
    <img
      src={product.image}
      alt={product.name}
      class="w-full aspect-[4/3] object-cover"
      loading="lazy"
      onerror="this.src='/images/products/placeholder.jpg'"
    />
  </div>

  <!-- 右: テキスト + スペック -->
  <div class="flex-1">
    <h3 class="font-serif text-xl border-b border-gray-200 pb-3 mb-4">
      ■ {product.name}　[{product.code}]
    </h3>

    <p class="text-sm text-gray-600 mb-6">{product.description}</p>

    <dl class="text-sm space-y-3">

      <!-- 粒度（nullでなければ表示） -->
      {product.specs.granularity && (
        <div class="flex gap-4 border-b border-gray-100 pb-3">
          <dt class="font-semibold text-gray-500 min-w-[80px] shrink-0">粒度</dt>
          <dd>{product.specs.granularity}</dd>
        </div>
      )}

      <!-- 分析値 -->
      <div class="border-b border-gray-100 pb-3">
        <dt class="font-semibold text-gray-500 mb-2">分析値</dt>
        <dd>
          <dl class="grid grid-cols-2 sm:grid-cols-3 gap-x-6 gap-y-1">
            {product.specs.analysis.map(item => (
              <div class="flex gap-2">
                <dt class="text-gray-500">{item.label}</dt>
                <dd>{item.value}</dd>
              </div>
            ))}
          </dl>
        </dd>
      </div>

      <!-- 嵩比重（nullでなければ表示） -->
      {product.specs.bulk_density && (
        <div class="flex gap-4 border-b border-gray-100 pb-3">
          <dt class="font-semibold text-gray-500 min-w-[80px] shrink-0">嵩比重</dt>
          <dd>{product.specs.bulk_density}</dd>
        </div>
      )}

      <!-- 補足（nullでなければ表示） -->
      {product.specs.notes && (
        <p class="text-xs text-gray-400 mt-2">{product.specs.notes}</p>
      )}

    </dl>
  </div>
</article>

【厳守事項】
- 製品カードのHTMLを手書きで繰り返さないこと。必ず .map() でループ生成すること
- null チェックは上記の通り条件付きレンダリングで対応すること
- public/images/products/placeholder.jpg を用意すること
  （Astroの public/ ディレクトリに 400x300 のグレー画像を1枚置く。
   sharp が使えれば生成、なければ https://placehold.jp/400x300.png を
   一時的に image の初期値として使ってもよい）