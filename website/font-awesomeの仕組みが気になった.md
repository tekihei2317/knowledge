# font-awesomeの仕組みが気になった

## font-awesomeの導入方法の確認

- CDNからCSSを読み込む
  - SVG+JSもあるみたい
- [Font Awesome](https://fontawesome.com/)から好きなアイコンを選んでコードをコピーする
  - SVGの場合も同じ?
  - ちなみにiタグのiはiconのiではなくitalicのiっぽい

  ```html
  <i class="fa fa-twitter"></i>
  ```

## 気になったところ

- WebフォントはCSSで出来ている?
  - Webフォント自体はどこかのサーバーに置かれていて、CSSでそれを読み込んで`font-family`を定義しているっぽい
  - `@font-face`を使うことで独自のフォントを定義できる
- クラスを指定するとアイコンが現れる原理
  - `fa`クラスを除外すると四角になった
  - `fa-twitter`クラスを除外するとそもそも表示されなかった
  - →両者はそれぞれどういう役割をしている?
- 文字を書いていないのにアイコンが出現すること
  - CSSでこのクラスを指定したとき、この文字を使うというようなことを定義している?
  - →多分そう。アイコンフォントを作ってみると分かりそう。

## 参考

- [Font Awesome 5 の使い方 / Web Design Leaves](https://www.webdesignleaves.com/pr/plugins/fontawesome_01.html)
- [【保存版】Font Awesomeの使い方：Webアイコンフォントを使おう](https://saruwakakun.com/html-css/basic/font-awesome)
- [Webアイコンフォントの作り方 - ③SASS/CSS、HTMLを設定する - Qiita](https://qiita.com/m-nakamura/items/0ec1b4144c514914d73f)
