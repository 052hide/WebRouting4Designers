---
marp: true
theme: gaia
_class: lead
paginate: true
---

# SPAとルーティング

---
## 全部/index.html

- `https://xxxxx.com` -> `/index.html`
- `https://xxxxx.com/articles` -> `/index.html`
- `https://xxxxx.com/articles/1` -> `/index.html`

全部同じindex.htmlにリダイレクトする

初回アクセス時以外のページ遷移はサーバーにリクエストしない
-> 早い、アニメーションをつけられる、状態を保持できるなどアプリっぽいことができる
-> 逆に初回アクセス時は基本的にフロントで必要な情報を全て取得するので遅い

---
## index.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <script type="module" crossorigin src="/assets/index.xxxxx.js"></script>
  </head>
  <body>
    <div id="root"></div>
  </body>
</html>
```

こんなようなHTMLになってることが多い

この場合、`#root` をSPAのDOMのルートとしてレンダリングする

---
## 問題

全部`/index.html`に飛ばされてしまったらメタ情報がページごとに出し分けできず、OGPやSEOに影響が出る。

---
## 最近のフレームワーク

ページごとにプリレンダリングしてくれることがある

プリレンダリングしておいてハイドレーションする

- `https://xxxxx.com`-> `/index.html`
- `https://xxxxx.com/articles` -> `/articles/index.html`

-> **静的なパスのページであれば**メタ情報の出し分けができる

---
## 動的なパスの場合は？

`https://xxxxx.com/articles/1` -> `/articles/[id]/index.html`

パスパラメータによるmeta情報の出し分けができない

---
## 対策

- SPAをやめる
- SSG
- SSR
- キャッシュを使う
- CDN Edgeでなんとかする

など

インフラの選定なども必要なことが多く、すべてそこそこ大掛かりな対応になる

---
## まとめ

シンプルなSPAでいいのか、できるだけはじめからちゃんと考えましょう
