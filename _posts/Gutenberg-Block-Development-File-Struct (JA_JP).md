# Gutenbergブロック開発 ファイル構成

## 概要

現在のGutenbergブロックは、ほぼ共通したファイル構成で作られています。

代表的な構成は次のようになります。

```text
my-block/
├── block.json
├── edit.js
├── save.js
├── render.php
├── index.js
├── editor.scss
├── style.scss
└── view.js
```

静的ブロックか動的ブロックかによって、使用するファイルは多少異なります。

私が開発している **Alfred Affiliate** は Dynamic Block のため、`render.php` を使用し、`save.js` は使用していません。

---

# 各ファイルの役割

## block.json

私はこれを **「設計図（Blueprint）」** と考えています。

ブロックの名前、属性、デフォルト値、使用するスクリプトやスタイルなど、ブロック全体の情報を定義します。

例えば、

```json
"title": {
    "type": "string",
    "default": "Masao's Lab"
}
```

と書くことで、

- React（edit.js）
- PHP（render.php）

の両方から `title` 属性を共通で利用できます。

### 主な役割

- ブロック名
- タイトル
- アイコン
- カテゴリ
- Attributes
- Default Values
- 使用する JavaScript
- 使用する CSS

---

## edit.js

Reactで作られた **エディター画面** です。

WordPress管理画面のブロックエディターで動作します。

ここでは、

- RichText
- TextControl
- MediaUpload
- InspectorControls
- ボタン
- React Components

などを使って編集UIを作ります。

つまり、

> **「WordPress管理画面で何を表示・編集するか」**

を作るファイルです。

---

## render.php

公開ページ側を担当するPHPです。

投稿を表示したとき、

```
https://example.com/article
```

で実際に表示されるHTMLを生成します。

ここでは、

- HTML生成
- esc_html()
- esc_url()
- Attributesの表示

などを行います。

つまり、

> **「訪問者が見るページ」**

を作るファイルです。

---

## index.js

WordPressへブロックを登録するためのエントリーポイントです。

このファイルが、

- block.json
- edit.js

を読み込み、

```javascript
registerBlockType(...)
```

によってブロックを登録します。

私はこれを

> **「接着剤」**

と考えています。

---

## style.scss

共通スタイルです。

このCSSは

- エディター
- 公開ページ

の両方で使用されます。

カードの見た目など、共通部分はこちらに記述します。

---

## editor.scss

エディター専用CSSです。

WordPress管理画面だけで使用されます。

例えば、

- 編集中だけ表示したい枠線
- プレースホルダー
- エディター専用レイアウト

などを書きます。

---

## save.js

Static Blockで使用されます。

投稿保存時にHTMLを生成し、そのHTMLが投稿本文に保存されます。

Dynamic Blockでは使用しません（render.phpを使用するため）。

---

## view.js

公開ページ用JavaScriptです。

ページ表示後に動作するJavaScriptを書きます。

例えば、

- ボタンクリック
- Ajax
- アニメーション
- API呼び出し

などを実装します。

必要なければ作らなくても構いません。

---

# Static Block と Dynamic Block

## Static Block

```text
Editor
    ↓
save.js
    ↓
HTMLを保存
    ↓
Frontend
```

保存時にHTMLを生成します。

---

## Dynamic Block

```text
Editor
    ↓
Attributes
    ↓
render.php
    ↓
HTML生成
```

ページ表示時に毎回HTMLを生成します。

Alfred Affiliateはこちらを採用しています。

---

# Alfred Affiliate の構成

```text
alfred-affiliate/
├── block.json      ← 設計図
├── edit.js         ← Reactによる編集画面
├── render.php      ← 公開ページ生成
├── index.js        ← ブロック登録
├── editor.scss     ← エディター専用CSS
├── style.scss      ← 共通CSS
└── view.js         ← 必要ならフロント側JavaScript
```

---

# 一番覚えておきたいこと

私は次のように覚えることにしました。

```text
block.json
      │
      ├───────────────┐
      │               │
      ▼               ▼
edit.js         render.php
(編集画面)       (公開画面)
      ▲               ▲
      └──── index.js ─┘
```

つまり、

- **block.json** = 設計図
- **edit.js** = 編集画面（React）
- **render.php** = 公開画面（PHP）
- **index.js** = 接着剤（ブロック登録）

まずはこの4つを理解すれば、Gutenbergブロック開発の全体像が見えてくる。
