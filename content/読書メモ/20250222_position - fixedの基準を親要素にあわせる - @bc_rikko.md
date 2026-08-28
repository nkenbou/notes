---
permalink: 751567725071
tags:
  - CSS
  - Tips
URL: https://bcrikko.github.io/til/posts/2025-02-22/position-fixed/
著者: ダーシノ (@bc_rikko)
公開日: 2025-02-22
開始日:
終了日:
---
# 読書メモ: position: fixedの基準を親要素にあわせる | @bc_rikko

- **URL:** [position: fixedの基準を親要素にあわせる | @bc_rikko](https://bcrikko.github.io/til/posts/2025-02-22/position-fixed/)
- **著者:** ダーシノ (@bc_rikko)
- **公開日:** 2025-02-22

## いつ読むか？

- CSS で `position: fixed` で親要素を基準にしたいとき

## 読書メモ

### 問題

`position: fixed` は通常 viewport 基準で配置される。親要素内で固定配置したい場合は工夫が必要。

### 解決方法

**方法1: transform (従来)**
```css
.parent {
  transform: translate(0);
}
```

**方法2: contain (推奨)**
```css
.parent {
  contain: layout;
}
```

### ポイント

- `contain: layout` の方が意図が明確で推奨
- 子要素は通常通り `position: fixed` を指定
