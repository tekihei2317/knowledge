# 住所をDBに保存するときのカラム名について

## 例

- 住所はFakerで作成
  - 県、市区町村、町名・番地、建物名で分割する
- とりあえずprefecture, city, block, buildingにした
  - blockが良くないかもしれない

```text
833-7035  高知県 | 野村市南区 | 宮沢町三宅10-4-10 | コーポ吉田103号
912-6237  群馬県 | 中島市南区 | 吉本町加納1-5-2   | ハイツ佐藤101号
408-4759  高知県 | 山口市西区 | 中島町伊藤9-1-1
```

## 参考

- [今どきの入力フォームはこう書く！ HTMLコーダーがおさえるべきinputタグの書き方まとめ - ICS MEDIA](https://ics.media/entry/11221/)
  - 補完を効かせるためには、address-level1, address-level2, address-line1, address-line2の4つを使うみたい
