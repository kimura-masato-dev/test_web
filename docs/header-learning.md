# ヘッダー制作で学んだこと

参考サイト（KURASHICOM風）をもとに、左ロゴ・右メニューのヘッダーを作る過程で学んだ内容のまとめ。

## 完成した HTML 構造

```html
<header id="header">
  <h1 class="logo"><a href="/">ロゴ</a></h1>

  <nav class="menu_list" aria-label="メインメニュー">
    <ul>
      <li><a href="#">会社概要</a></li>
      <li><a href="#">サービス</a></li>
      <li><a href="#">制作実績</a></li>
      <li><a href="#">採用情報</a></li>
    </ul>
  </nav>
</header>
```

### 構造のポイント

| 要素 | 役割 |
|------|------|
| `<header>` | ページ上部のヘッダー領域 |
| `<h1 class="logo">` | サイト名・ロゴ（ページでいちばん重要な見出し） |
| `<nav>` | ナビゲーションであることを意味づけ |
| `<ul><li>` | メニュー項目のリスト |
| `<a>` | 各ページへのリンク |

**`nav > ul > li > a` の形で右メニューを作る方向性は正しい。**

---

## 1. ヘッダーのレイアウト（Flexbox）

```css
#header {
  display: flex;
  align-items: center;  /* 直接の子（h1, nav）を縦中央に */
  padding: 0 80px;
  height: 80px;
}

#header .menu_list {
  margin-left: auto;  /* 右寄せ */
}

#header .menu_list ul {
  display: flex;      /* li を横並びに */
  gap: 32px;          /* メニュー間の余白 */
}
```

### 覚えておくこと

- `display: flex` + `margin-left: auto` で「左ロゴ・右メニュー」が作れる
- **`align-items: center` は「その要素の直接の子」にしか効かない**
- 入れ子が深いほど、必要な階層ごとに flex を指定する

```
#header          → h1 と nav を横並び・縦中央
  .menu_list     → ul を縦中央（display: flex + align-items: center）
    ul           → li を横並び（display: flex）
```

### よくあるハマりどころ

`.menu_list` に `display: flex` を付けたらメニューが縦並びになった場合：

- `nav` の直接の子は `ul` だけ（1個）
- **`li` を横並びにしているのは `ul` の `display: flex`**
- `.menu_list` に flex を足しても、`ul` 側の flex を消すと `li` は縦並びに戻る
- **両方に flex が必要（役割が違う）**

---

## 2. リンク（`href`）の意味

### `href="/"`

サイトのトップページ（ルート）へのリンク。

- `https://example.com/` の `/` 部分と同じ意味
- ロゴクリックでトップに戻る、という一般的な動き

ローカルで `file://` 直開きだと動かないことがある。学習中は `href="index.html"` でも可。

### `href="#"`

- 同じページ内の先頭へスクロールする
- ページがまだないときの**仮リンク**としてよく使う
- 本番では実際の URL に差し替える

---

## 3. `aria-label="メインメニュー"`

スクリーンリーダーなどの支援技術に、「このナビの名前」を伝えるための属性。

- 画面上には表示されない
- 必須ではないが、付けておくとアクセシビリティが上がる
- ヘッダー・フッターなど `<nav>` が複数あるときに特に有用

---

## 4. リンクの下線を消す

`h1` に下線があるように見えても、原因は **中の `<a>` タグ**。

```css
a {
  color: inherit;
  text-decoration: none;  /* 下線を消す */
}
```

### 注意：`text-align` と `text-decoration` の違い

| プロパティ | 役割 |
|-----------|------|
| `text-align` | 文字の揃え（左・中央・右） |
| `text-decoration` | 下線・取り消し線など |

`text-align: none` は存在しない。下線を消すには `text-decoration: none`。

---

## 5. ホバー効果

```css
#header .menu_list a {
  transition: opacity 0.3s ease; /* 任意：なめらかに変化 */
}

#header .menu_list a:hover {
  opacity: 0.8;
}
```

| 指定 | 必要？ | 効果 |
|------|--------|------|
| `opacity: 0.8`（`:hover`） | 必要 | ホバー時に少し透明に |
| `transition` | 任意 | 変化を 0.3 秒でなめらかに |

- ホバーはクリック対象の `<a>` に付ける
- `transition` がなくてもホバーは動く（パッと切り替わる）

---

## 6. コーディングの効率化（Emmet）

メニューを1つずつ書かずに、Emmet で一括生成できる。

```
ul>li*4>a[href="#"]
```

Tab で展開 → 4 つの `<li><a>` が一度にできる。

テキストまで入れる例：

```
ul>(li>a[href="#"]{会社概要}+li>a[href="#"]{サービス}+li>a[href="#"]{制作実績}+li>a[href="#"]{採用情報})
```

---

## 7. 今後の改善ポイント

- [ ] `.menu_list` に `display: flex` を追加して `ul` の縦中央寄せを完成させる
- [ ] `href="#"` を実際のページ URL に差し替える
- [ ] スマホ対応（ハンバーガーメニューなど）
- [ ] ヒーローセクション（大きな画像＋キャッチコピー）の追加

---

## 関連ファイル

- `index.html` … ヘッダーの HTML
- `assets/css/style.css` … リセット CSS + ヘッダースタイル
