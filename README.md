# SlickNav の使用方法（組み込み事例）

ハンバーガーメニューに`SlickNav`を使用して以下のようなメニューを作成します。

![](https://i.gyazo.com/b278626f981e262692ad3cfee1560681.gif)

`SlickNav`は[公式サイト](https://computerwolf.github.io/SlickNav/) で無料で配布されているハンバーガーメニューを実現する仕組みです。
`SlickNav`を使用すればハンバーガーメニューを比較的簡単に実装することができます。

この文章では以下の内容を順番に説明します。

1. `SlickNav`の組み込み方法
	- 基本的な組み込み方法
	- オプションの指定
2. `SlickNav`の見た目のカスタマイズ

## 1. `SlickNav`の組み込み方法 - 基本的な組み込み方法

この章ではこのような見た目を作ります

![](https://i.gyazo.com/9d8fba6733cc30fe4d322dc2f5e36a31.gif)

`SlickNav`の使用方法は[公式サイト](https://computerwolf.github.io/SlickNav/)（及び[公式GitHubリポジトリー](https://github.com/ComputerWolf/SlickNav#usage)）に記載されており、それに従って設置作業を進めていきます。

（[公式サイト](https://computerwolf.github.io/SlickNav/)は「分かる人向け」に省略して書かれているため、そのままでは初心者には厳しい内容になっています。`Google`検索で`SlickNav`の日本語の解説記事を探し、それを頼りに作業するとよいでしょう。）

`SlickNav`を組み込む前の`HTML`を以下のように用意します。`SlickNav`ではメニューとしてリストを使用しますので、`ul`としてマークアップしました。

```
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <title>SlickNav 組み込み事例</title>
</head>
<body>
  <ul>
    <li><a href="">森林探検隊</a></li>
    <li><a href="">季節のイベント</a></li>
    <li><a href="">アクセスマップ</a></li>
    <li><a href="">お問い合わせ</a></li>
    <li><a href="">ブログ</a></li>
  </ul>
</body>
</html>
```

`SlickNav`を組み込んだ後は次のようになります。

```index1.html
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <title>SlickNav 組み込み事例</title>
  <!-- 1 -->
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.4/jquery.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/SlickNav/1.0.10/jquery.slicknav.min.js"></script>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/SlickNav/1.0.10/slicknav.min.css" />
</head>
<body>
  <!-- 2 -->
  <ul>
    <li><a href="">森林探検隊</a></li>
    <li><a href="">季節のイベント</a></li>
    <li><a href="">アクセスマップ</a></li>
    <li><a href="">お問い合わせ</a></li>
    <li><a href="">ブログ</a></li>
  </ul>
  <!-- 3 -->
  <script>
    $(function(){
      $('ul').slicknav();
    });
  </script>
</body>
</html>
```

`HTML`のコメント`<!-- 1 -->`〜`<!-- 3 -->`の３箇所に組み込み作業を行っています。
以下説明します。

1. `<!-- 1 -->` の箇所 ... `SlickNav`を構成する以下の３ファイルを読み込んでいます。
	- a. `jQuery`本体
	- b. `SlickNav`本体
	- c. `SlickNav`用のCSS
2. `<!-- 2 -->` の箇所 ... `SlickNav` の素材となる`<ul>` を用意します
3. `<!-- 3 -->` の箇所 ... 閉じタグ`</body>` の直前に`SlickNav` を起動する`<script> `（`JavaScript`プログラム）を入れます

この`<!-- 1 -->`から`<!-- 3 -->`の作業は全て[公式サイト](https://computerwolf.github.io/SlickNav/)（及び[公式GitHubリポジトリー](https://github.com/ComputerWolf/SlickNav#usage)）に従った内容となっています。

## 1. `SlickNav`の組み込み方法 - オプションの指定

上記で説明した基本的な利用方法を使用した上で、オプションの設定を追加することが可能です。

（指定できるオプションは[公式サイト](https://computerwolf.github.io/SlickNav/)の「Available Options（利用可能なオプション）」に説明があります。）

### オプション - 「MENU」を消す

アイコンの左側に表示されている「MENU」の文字を消してアイコンだけの表示にするために、<!-- 3 --> にラベルオプション（`label`）を追加します。

```index2.html
<script>
  $(function(){
    $('ul').slicknav({
      label: '',
    });
  });
</script>
```
（この書式を正確に理解するには`JavaScript`の知識が必用です。ここでは「こんなふうに書けばいいのだな」と流していただければ十分です）

「MENU」の文字が消えました。
![](https://i.gyazo.com/84bfdb310cb49e6924caf22fed7ce903.png)

### `.slicknav_menu` の挿入位置を調整します(`appendTo`オプション)
（このオプションについては後の方で説明します。）

## 2. `SlickNav`の見た目のカスタマイズ

`SlickNav`はハンバーガーメニューを表示するために`HTML`に`div`を追加します。
見た目のカスタマイズを行う準備として、具体的にどんなマークアップが追加されたかをデベロッパーツールを使用して確認しておきます。

### デベロッパーツールから、追加されたマークアップを調べておく

デベロッパーツールから調べると`<div class="slicknav_menu">`が追加されていることがわかります。
![](https://i.gyazo.com/d43d1d46d14a31906262be863044a761.png)

この`<div class="slicknav_menu>`の中を開いてみると、以下のような構造になっています。
```
<div class="slicknav_menu">
  <a href="#" aria-haspopup="true" role="button" tabindex="0" class="slicknav_btn slicknav_open" style="outline: none;">
    ...略...
  </a>
  <ul class="slicknav_nav" aria-hidden="false" role="menu" style="">
    <li><a href="" role="menuitem" tabindex="0">森林探検隊</a></li>
    <li><a href="" role="menuitem" tabindex="0">季節のイベント</a></li>
    <li><a href="" role="menuitem" tabindex="0">アクセスマップ</a></li>
    <li><a href="" role="menuitem" tabindex="0">お問い合わせ</a></li>
    <li><a href="" role="menuitem" tabindex="0">ブログ</a></li>
  </ul>
</div>
```

このうち、`a`要素（`a.slicknav_btn`）はハンバーガーメニューのアイコンの部分に相当し、`ul.slicknav_nav`がアイコンをクリックしたときにプルダウン表示されるメニュー本体になります。

マークアップの構造が把握できましたので、これを念頭に置いてカスタマイズ作業を行っていきます。

### `Desktop`と`Mobile`とで通常のナビゲーションとハンバーガーメニューとの表示を切り替える

画面幅が`Mobile`（スマートフォン、`600px`以下）の時はハンバーガーメニューだけを出し、逆に`Desktop(PC)`（`601px`以上）の時は通常のナビゲーション(`ul`の部分)だけを表示するようにします。

`SlickNav`が追加するハンバーガーメニューのクラス名は`.slickNav_menu`であると既にわかっています。

従って、
```
.slicknav_menu {
  display: none;
}
```
とすればハンバーガーメニューを非表示にすることができます。

これをもとに`Mobile`と`Desktop`で表示するものを切り替える`CSS`のコードは以下のようになります。

```index3.html
<style>
    /* Desktop */
    ul             { display: block; } /* `block`は`display`の初期値なのでこの一行は省略可能です */
    .slicknav_menu { display: none; }

    /* Mobile */
    @media (max-width: 600px) {
      ul             { display: none; }
      .slicknav_menu { display: block; }
    }
</style>
```

（一般的に、レスポンシブで画面幅に応じて表示するものを切り替える時にはこの手法を使います）

`Desktop`と`Mobile`でナビゲーションが切り替わるようになりました。
![](https://i.gyazo.com/780404bdbfdf1cf0d2c7a8d8df6ff91f.gif)

### `.slicknav_menu` の挿入位置を調整します(`appendTo`オプション)

目を整えるために、少々`HTML`を編集します。
`<header>`を加え、そのなかに`<h1>`を配置しなおしました。

```
<header>
  <h1>Green Camp</h1>
  <ul>
    <li><a href="">森林探検隊</a></li>
    <li><a href="">季節のイベント</a></li>
    <li><a href="">アクセスマップ</a></li>
    <li><a href="">お問い合わせ</a></li>
    <li><a href="">ブログ</a></li>
  </ul>
</header>
```

この`HTML`をプレビューすると、`SlickNav`は `<body>`先頭に追加されています。
![](https://i.gyazo.com/4e4f7502e28eaaefd15079a958c2000f.png)

この`SlickNav`の位置を変更してみたいと思います。
`SlickNav`には自身を挿入する場所を指定できるオプション（`appendTo`、〜の後に追加する）がありますので、これを使用して指定します。

```
<script>
  $(function(){
    $('ul').slicknav({
      label: '',
      appendTo: 'header',
    });
  });
</script>
```

（この書式を正確に理解するには`JavaScript`の知識が必用です。ここでは「こんなふうに書けばいいのだな」と流していただければ十分です）

`<header>`の末尾に追加されるようになりました。
![](https://i.gyazo.com/cfc647ca5dc00aa65cefaca74bbbc5db.png)

#### ハンバーガーメニューのアイコンだけにする

ハンバーガーメニューが横に長く伸びていますが、これをアイコンだけの短い表示に切り替えたいと思います。
次の`CSS`を加えます。

```
.slicknav_menu {
  background: transparent;
} 
```

アイコンだけになりました。
![](https://i.gyazo.com/4bdf5edbc05e90ddda7a658c56403a93.png)

（ここ以降の「見た目の調整」作業は、デベロッパーツールを用いて何に対しどんなプロパティを加えたら良いかを調査しながら行っています。`CSS`を書き換えて実験することが容易なデベロッパーツールはたいへん有用です。デベロッパーツールを活用しましょう。）

#### アイコン位置を調節し、`h1`の横に並べる

アイコンの位置を調節するために`position`プロパティを使用します。

以下の`CSS`を追加します。
```
header {
  position: relative;
}

.slicknav_menu {
  background: transparent;
  position: absolute;
  top: 0px;
  right: 0px;
} 
```
アイコンの位置が変わりました。
![](https://i.gyazo.com/09fe10ab6ae2273216ed0784556f63cc.png)

#### アイコンクリック時のプルダウンメニューの背景色を設定する

背景色が初期のままだと、プルダウンメニューが表示されても見えません。
![](https://i.gyazo.com/b2a94d55efe7cf832f2c3867e4018946.png)

`CSS`で背景色を与えましょう。
```
.slicknav_nav {
  background: #4c4c4c;
}
```

背景色を引いたことにより、内容が見えるようになりました。
![](https://i.gyazo.com/534ebad4630121c2740e726718774503.png)

## 完成版のソースコード

最終的にソースコードは以下のようになりました。

```index.html
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>SlickNav 組み込み事例</title>
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.4/jquery.min.js"></script>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/SlickNav/1.0.10/slicknav.min.css" />
  <script src="https://cdnjs.cloudflare.com/ajax/libs/SlickNav/1.0.10/jquery.slicknav.min.js"></script>
  <style>
    /* Desktop */
    ul             { display: block; }
    .slicknav_menu { display: none; }

    /* Mobile */
    @media (max-width: 600px) {
      ul             { display: none; }
      .slicknav_menu { display: block; }

      header {
        position: relative;
      }

      .slicknav_menu {
        background: transparent;
        position: absolute;
        top: 0px;
        right: 0px;
      } 

      .slicknav_nav {
        background: #4c4c4c;
      }
    }
  </style>
</head>
<body>
  <header>
    <h1>Green Camp</h1>
    <ul>
      <li><a href="">森林探検隊</a></li>
      <li><a href="">季節のイベント</a></li>
      <li><a href="">アクセスマップ</a></li>
      <li><a href="">お問い合わせ</a></li>
      <li><a href="">ブログ</a></li>
    </ul>
  </header>
  <script>
    $(function(){
      $('ul').slicknav({
        label: '',
        appendTo: 'header',
      });
    });
  </script>
</body>
</html>
```

## まとめ

`SlickNav`の基本的な使い方（組み込み方）を紹介し、`SlickNav`の見た目の調整の方法を説明しました。
