## PHASE 1: Tailwind カスタムテーマ と グローバルCSS の設定

### tailwind.config.ts に追加するカスタムカラー
{
  colors: {
    primary:     '#B22222',  // 朱色（メインアクセント）
    dark:        '#1A1A1A',  // 墨色（テキスト・暗背景）
    light:       '#FFFFFF',  // 白（ベース背景）
    'off-white': '#F5F5F0',  // セクション背景用オフホワイト
  }
}

### Google Fonts（Layout.astroの<head>内に追加）
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@400;500;700&family=Noto+Serif+JP:wght@400;700&display=swap" rel="stylesheet">

Tailwind の fontFamily に以下を追加:
- sans:  ['Noto Sans JP', 'sans-serif']
- serif: ['Noto Serif JP', 'serif']

### src/styles/global.css
html { scroll-behavior: smooth; }
body { @apply font-sans text-dark bg-light; }
h1, h2, h3 { @apply font-serif; }