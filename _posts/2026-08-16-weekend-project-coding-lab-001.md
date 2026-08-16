---
layout: post
title: "Weekend Project Coding Lab 001 Hello TypeScript"
date: 2026-08-16
---

# Weekend Project - Coding Lab 001

## 雑談部分

**現代のフロントエンドの典型的な役割分担**
1. TypeScript: ロジック
2. JSX: 構造
3. CSS: 表現

- ロジック部分にPythonを使うことも一般的。Swiftを使うことも
  
```text
Frontend
================
HTML
CSS
JavaScript
TypeScript
React

Backend
================
Python
Java
Go
Node.js
.NET

Data / AI
================
Python
SQL
LLM
```

- tsx = ロジック＋UI構造＋データの流れ
- CSS = 見た目＋レイアウト＋表現
- アプリケーション = TypeScript/TSX + CSS + Assets

```text
Component
├── Structure
│      JSX
├── Logic
│      TypeScript
└── Style
       CSS
```

SwiftUIとReactの比較
| | SwiftUI | React |
|-|-|-|
| macOSネイティブ感 | ◎ | △ |
| Web共有 | △ | ◎ |
| クロスプラットフォーム | △ | ◎ |
| Apple API連携 | ◎ | △ |
| UI開発速度 | ○ | ◎ |

## 学習メモ

- code . は親ディレクトリではなく、該当タスクのディレクトリで実行する
- const: 定数、ほとんどこれ、let: 値が変化するときのみ、var: 基本使わない

```bash
# JavaScriptの実行環境のversion check
node --version

# TypeScriptをJavaScriptに変換するコンパイラのversion check
tsc --version

# Globa/Projectに導入されているか確認
which tsc
npm list -q --depth=0

# npm 初期化
npm init -y

# typescriptをプロジェクト単位でインストール
npm install --save-dev typescript

# typescriptのversion check
npx tsc --version

# もしグローバルにインストールする場合
npm install -g typescript
```
- package.json: プロジェクトの設計書（メタ情報＋依存関係管理ファイル）
 npm →　package.jsonを見る →　script実行

TypeScript コンパイル　→　実行の流れ

1. hello.ts を作る
2. npx tsc hello.ts でコンパイル
3. hello.js を確認
4. node hello.js で実行

- 型推論は、内部変数では推論に任せる、外部境界では型を書く
- interfaceでデータ構造の設計図を作る
- Data: JSON + 型定義: TS interface + 表示: React
- User Data (JSON) →　interface →　function (React) →　output
- データと処理を分離する設計

```bash  
# 毎回、hello.jsを削除するのは面倒なため、tsconfig.jsonを作成し、dist/にhello.jsを出力
# tsconfig.jsonを作成
npx tsc --init
Created a new tsconfig.json

#tsconfig.jsonを編集
{
  "compilerOptions": {
    "target": "...",
    "module": "...",
    "outDir": "./dist"
  }
}

```
この設定のあとは、npx tscでコンパイル
`npx tsc` tsconfig.jsonの設定通りにプロジェクト全体をコンパイルしてという意味
`node dist/hello.js` これで実行


### hello.ts

```TypeScript
// 現代TypeScriptでは基本constを使う
// 値が変化する場合だけletを使う
// 内部変数は型推論に任せることが多い
const msg: string = "Hello Alfred!!!"
const message = "Hello TypeScript"
const age = 50

// 型を明示、letは後代入可能
let category: string

if (age >= 40) {
    category = "Senior"
} else {
    category ="Young"
}

// 現代的な書き方
// const category = age >= 40 ? "Senior" : "Young"

// const age: number = "50" ## わざと間違える
// consoleの表示機能で表示
console.log(msg)
console.log(message)
console.log(age)
console.log(category)

// 関数の定義

function greet(name: string) {
    return `Hello ${name}`
}

const result = greet("Smith")

console.log(result)

// オブジェクト (interface)

interface User {
    name: string
    age: number
    role: string
}

const user: User = {
    name: "Masao",
    age: 50,
    role: "Software Designer"
}

console.log(user)
console.log(user.role)

// interface + function

function showUser(user: User) {
    return `${user.name} (${user.role})`
}

const userInfo = showUser(user)

console.log(userInfo)

// interface, 配列, 型, arrow function, forEach

```

### 学習範囲のまとめ

```text
TypeScript Coding Lab #001

環境
├── Node.js
├── npm
├── package.json
├── node_modules
├── tsconfig.json

言語基礎
├── const
├── let
├── 型注釈
├── 型推論

実行モデル
├── .tsを書く
├── tscでコンパイル
├── .js生成
├── nodeで実行

プログラム構造
├── function
├── parameter
├── return

データモデル
├── object
├── interface
├── type contract
```