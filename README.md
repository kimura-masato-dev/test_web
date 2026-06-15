# html/css を学ぶ場所

HTML/CSS のレイアウト練習用リポジトリ。

## 現在の構成

- `index.html` … ヘッダー（ロゴ + メニュー領域）
- `assets/css/style.css` … リセットCSS + ヘッダーのレイアウト

## 学んだこと

### 1. 何も表示されない理由

- `<title>` はタブに表示されるが、**ページ本文とは別**
- `<h1>` や `<div>` の中身が空だと、**高さがほぼ 0** になる
- `background-color` だけ指定しても、要素に高さがなければ見えない

**対策（レイアウト練習用）**

- `height` または `min-height` を指定する
- 色で区切りたいときは `background-color` を使う（`color` は文字色のみ）

### 2. クラス名は HTML と CSS で完全一致させる

| 場所 | クラス名                      |
| ---- | ----------------------------- |
| HTML | `menu_list`（アンダースコア） |
| CSS  | `.menu_list`                  |

`menu_list` と `menu-list` は別物なので、スタイルが当たらない。

### 3. ヘッダーを左右に配置する

````css ① padding 指定
#header {
  display: flex;
  align-items: center;
  padding: 0 80px; /* 左右の内側余白 */
}

#header h1 {
  color: azure;
  font-size: 24px;
  background-color: brown;
}

#header .menu_list {
  margin-left: auto; /* 右寄せ */
}

```css ② 各子要素margin 指定 #header {
  display: flex;
  align-items: center;
}

#header h1 {
  color: azure;
  font-size: 24px;
  background-color: brown;
  margin-left: 80px;
}

#header .menu_list {
  margin-left: auto; /* 右寄せ */
  margin-right: 80px;
}
````
