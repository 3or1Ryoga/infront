## データ差し替え手順

### 製品データ
1. クライアントからExcel/CSVを受け取る
2. Claude CodeにPHASE 5.5の指示とExcelの内容をコピペして投げる
3. 出力されたJSONでsrc/data/products.jsonを上書き
4. npm run build でビルド確認

### 製品画像
1. クライアントから画像ファイルを受け取る
2. public/images/products/ に配置
3. products.jsonの "image" パスを実ファイル名に更新
   例: "/images/products/TBA-001.jpg"

### 会社情報（電話・住所・メール等）
1. src/data/site.ts の SITE定数を更新するだけ
2. 全ページに自動反映される

### ヒーロー背景画像
1. クライアントから写真素材を受け取る
2. public/images/hero.jpg に配置
3. トップページのHeroセクションの背景を
   bg-dark から bg-[url('/images/hero.jpg')] bg-cover bg-center に変更