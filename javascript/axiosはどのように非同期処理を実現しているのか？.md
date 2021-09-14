# axiosはどのように非同期処理を実現しているのか？

## 疑問点

```javascript
axios.get('/user?ID=12345')
  .then(function (response) {
    console.log("debug 1");
  })
console.log("debug 2");
```

実行結果

```text
debug 2
debug 1
```

気になったのは`get`メソッドをどのように実装すれば、このように処理が終わる前に次に処理を移すことが出来るのか、ということ。

## 解決した

async関数を使えば実現できる。async関数はその名前の通り非同期で処理を実行する関数。async関数をawaitを書かずに実行すると、処理が終わる前に次に処理が移る。

```javascript
async function get() {
  // 3秒待つ
  await new Promise((resolve) => setTimeout(resolve, 3000));

  return "debug 1";
}

get().then((value) => {
  console.log(value);
});

console.log("debug 2");
```

実行結果

```bash
debug 2
debug 1 # 3秒後
```

axiosのget関数の中身は、Promiseの中でリクエストを送る、レスポンスを受け取る（レスポンスが返ってくるまでどうやって待っているかは謎）、レスポンスを解析する、ということをやっているのだと思う。

残る疑問点はasyncは内部的にどういうことをしているのか、asyncを使わずに同様のことを実現するにはどうすればいいのか、ということ。これは奥が深い気がするのでここらへんで撤退する。

## 参考

参考になりそうな資料

- [非同期処理ってどういうこと？JavaScriptで一から学ぶ - Qiita](https://qiita.com/kiyodori/items/da434d169755cbb20447)
- [JavaScript イベントループの仕組みをGIFアニメで分かりやすく解説 | コリス](https://coliss.com/articles/build-websites/operation/javascript/javascript-visualized-event-loop.html)
  - asyncは内部的にはこういうことをしているのかもしれない
