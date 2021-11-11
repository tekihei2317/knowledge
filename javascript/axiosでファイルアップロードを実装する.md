# axiosでファイルアップロードを実装する

axiosのドキュメントにはブラウザでは`File`・`FormData`・`Blob`が送れると書いてあったが、`File`で送ると空のオブジェクトが送信されていてうまくいかなかった。`FormData`で送るとうまくできたのでメモしておく。

Vueのテンプレート

```html
<input type="file" @change="onFileChange">
```

Vueのmethods

```javascript
onFileChange(event) {
  const file = event.target.files[0];
  this.detailedStatementFile = file;

  const formData = new FormData();
  formData.append("file", file);

  const endpoint = '<endpointを入れる>';
  axios.post(endpoint, formData);
},
```

上記の場合はキーが`file`で送られるので、バックエンドからはそのキーで取得できる。

## 参考

- [axios/axios: Promise based HTTP client for the browser and node.js](https://github.com/axios/axios)
- [axios で添付ファイルありのリクエスト(multipart/form-data の POST) - to-me-mo-rrow - 未来の自分に残すメモ -](https://r17n.page/2020/02/04/nodejs-axios-file-upload-api/)