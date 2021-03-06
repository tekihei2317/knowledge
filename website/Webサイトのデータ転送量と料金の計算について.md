# Webサイトのデータ転送量と料金の計算について

## データ転送量とは

- サーバーから送られるデータの量。Webサイトの場合はChromeのDevToolsのNetworkタブのtransferから確認できる
- 一般的なWebサイトだと1ページ1MBくらいな気がする。画像が大きく占めている気がする。
  - 最適化?するとNetworkタブで`disk cache`という表示がされて、転送量に加算されないっぽい
- 英語だとbandwidth。直訳すると帯域幅だけど、帯域幅=転送量っぽいので同じ意味。

## 料金の計算

### GitHub Pages

- ホスティングするWebサイトの容量は1GBまで
  - HTML、CSS、JS、画像の合計だと思う
- GitHub Pagesは100GB/月まで無料
  - 超えると多分Webサイトが見れなくなる
- 1ページを1MBとすると、100GB / 1MB = 100000PVまで
- 参考
  - [About GitHub Pages - GitHub Docs](https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages)

### Netlify

- 無料プランは100GB/月まで無料で、それ移行は100GBごとに$20
- 1ページを1MBとすると、GitHub Pagesと同様に10万PVまで無料。
- それ以降は10万PVごとに約2000円なので、100万PVだと1万8000円かかる
  - ちょっと高い（これぐらいの規模だったら、痛くも痒くもない気はするが）
- 参考
  - [Netlify Pricing and Plans](https://www.netlify.com/pricing/)

### Amazon S3

- 従量課金。主にストレージ容量、データ転送量、リクエスト数に対して課金される。

| 種類          | 料金                        |
| ------------- | --------------------------- |
| ストレージ    | 0.025USD / GB               |
| GETリクエスト | 0.00037USD / 1000リクエスト |
| データ転送量  | 0.114USD/GB                 |

- 容量が1GB、100万PV=データ転送量1000GBで計算する
  - データ転送量以外は雀の涙(100円未満)
  - データ転送量はやっぱりNetlifyと同じくらいで1万円を超える
    - 0.114USD x 1000 = $1140 = 1万1140円
- 参考
  - [料金 - Amazon S3 ｜AWS](https://aws.amazon.com/jp/s3/pricing/?nc=sn&loc=4)
  - [S3の料金を日本円でざっくり計算 | ざっくりAWS](https://aws-rough.cc/s3/)

## まとめ

- 静的Webサイトのホスティングにかかえるお金で大きな割合を占めるのはデータ転送量
- 画像をいい感じにすることで、1ページあたりのデータ転送量を抑えることが出来そう

## 参考

- [データ転送量 | レンタルサーバー　Bizメール＆ウェブ ビジネス | NTTコミュニケーションズ 法人のお客さま](https://www.ntt.com/business/services/cloud/rental-server/biz/function/traffic.html)
- [AWSの料金の目安になるかも！？Webサイトのデータ転送量を調べてみる | 株式会社ビヨンド](https://beyondjapan.com/blog/2016/03/howmuch-traffic-data/)
