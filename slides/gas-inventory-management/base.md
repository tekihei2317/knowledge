---
marp: true
theme: gaia
footer: by ＠tekihei2317
---

# GASで在庫管理をサクッと実装した話

---

## 目次

1. ある日のこと
2. Google App Script（GAS）とはなにか
3. 先入れ先出し法について
4. 作ったプログラム
5. claspでローカルでGASを書く
6. まとめ

---

## ある日のこと

上長「在庫管理したいんだけど、スプレッドシートでこれ出来る？」
上長「先入れ先出し法っていうのがあって...」
ぼく「なるほど...」

~~ 30分後 ~~

ぼく「スプレッドシートだと難しいと思います！」
ぼく「これはプログラムを書きたくなるやつですね」

---

## ある日のこと（続き）

~~ その日の夜 ~~

ぼく「あ！そういえばGASがあったわ！作っちゃお！！」

~~ 翌日の朝 ~~

ぼく「なんかできた！！」

---

## できたもの

---

## Google App Script（GAS）とは

- Googleのサービスと連携したアプリケーションを作るためのプラットフォーム
  - Gmail、Google Drive、Google Calender、etc...

- JavaScriptで書ける！
  - 処理系がChromeと同じV8エンジン

---

## 先入れ先出し法について

---

## 作ったプログラム（入力）

在庫の個数と価値のペアをシートから読み込む

```javascript
const makeStocks = (lastRowIndex) => {
  const stocks = [];
  for(let i = OFFSET_ROW; i <= lastRowIndex; i++){
    const count = sheet.getRange(i, OFFSET_COL).getValue();
    if (count > 0) {
      const price = sheet.getRange(i, OFFSET_COL + 1).getValue();
      stocks.push({ count, price });
    }
  }
  return stocks;
};
```

---

## 作ったプログラム（計算）

ちょっと長いので省略

```javascript
// TODO:
```

---

## 作ったプログラム（出力）

計算した値をセルに出力する

```javascript
const setPriceSum = (priceSumList) => {
  priceSumList.forEach((priceSum, index) => {
    // 開始行は固定値なので、その次の行から埋める
    sheet.getRange(OFFSET_ROW + 1 + index, CONSUMED_COUNT_COL + 1).setValue(priceSum);
  });
}
```

---

## 作ったプログラム（トリガーの設定）

セルを変更したときに計算を実行する

```javascript
// TODO: onEditにする
const main = () => {
  const lastRowIndex = calcLastRowIndex();
  const stocks = makeStocks(lastRowIndex);
  const priceSumList = calcCounsumedPriceSum(stocks, lastRowIndex);
  setPriceSum(priceSumList);
};
```

---

## claspでローカルでGASを書く

今回のリポジトリ: TODO:

---

## まとめ

- GASはJSで書けるのでとても便利
- めんどくさいことがあれば自動化するのでまかせてください！！

---

## 参考サイト

- [GAS（Google Apps Script）入門｜エクセルの神髄](https://excel-ubara.com/apps_script1/)
- [GAS のGoogle謹製CLIツール clasp - Qiita](https://qiita.com/HeRo/items/4e65dcc82783b2766c03)
