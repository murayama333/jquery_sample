# jQueryとは

jQueryは高速で軽量で多機能なJavaScriptライブラリです。HTMLドキュメントのトラバーサル、マニュピレーション、イベントハンドリング、アニメーション、Ajaxなどを簡単に実行できます。jQueryはほとんどのモダンなブラウザで動作します。jQueryは汎用性のがある拡張しやすい実装になっています。

> トラバーサルは横断、マニュピレーションは操作という意味です。

## 3つの特徴

### Lightweight Footprint

ミニファイしてgzipするとわずか32kBです。AMDモジュールとして利用することもできます。

### CSS3対応

CSS3で提唱されているセレクタによるトラバーサルをサポートしています。

http://wp-e.org/2014/05/20/2420/

### クロスブラウザーサポート

概ね、、最新のバージョンと一つまえのバージョンを公式にサポートしています。

Desktop
  + Chrome: (Current - 1) and Current
  + Edge: (Current - 1) and Current
  + Firefox: (Current - 1) and Current
  + Internet Explorer: 9+
  + Safari: (Current - 1) and Current
  + Opera: Current
+ Mobile
  + Stock browser on Android 4.0+
  + Safari on iOS 7+


## コードの概要

### DOM Traversal and Manipulation

class属性がcontinueのbuttonタグを取得（トラバース）して、HTMLを'Next Step'に変更（マニュピレート）するには次のように実装します。

```javascript
$( "button.continue" ).html( "Next Step..." )
```

> jQueryでは$()という記述を多用します。$()の実体は関数呼び出しです。$()はjQuery()と置き換えることもできます。

### Event Handling

CSSによってdisplay:noneが指定されている #banner-message 要素をクリックしたときに、画面に表示するには次のように実装します。

```javascript
var hiddenBox = $( "#banner-message" );
$( "#button-container button" ).on( "click", function( event ) {
  hiddenBox.show();
});
```

### Ajax

クエリパラメータzipcode=97201を指定して"/api/getWeather"を呼び出し、結果を#weather-temp要素に表示するには次のように実装します

```javascript
$.ajax({
  url: "/api/getWeather",
  data: {
    zipcode: 97201
  },
  success: function( result ) {
    $( "#weather-temp" ).html( "<strong>" + result + "</strong> degrees" );
  }
});
```

## jQueryのインストール

CDN経由でjQueryを使用する場合は次のように実装します。

### Google CDN

```html
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js"></script>
```

### ローカルにダウンロードする場合

以下のページからダウンロードできます。

http://jquery.com/download/


## $(document).ready()

jQueryでHTMLのマニュピレートを実行するには、HTMLドキュメントの全体の読み込みが終了するのを待つ必要があります。jQueryのready関数を使うとHTMLドキュメント読み込み時に任意のJavaScriptコードを実行できます。

```javascript
$( document ).ready(function() {
    console.log( "ready!" );
});
```

上記のコードは少し長くて読みにくいので、以下のように実装することが推奨されています。

```javascript
$(function() {
    console.log( "ready!" );
});
```

> 参考: https://learn.jquery.com/using-jquery-core/document-ready/

## ハンズオン

### sample1.html

jQueryが正しく動作するか確認します。

+ CDNからjQueryをダウンロードしています。
+ $(document).ready()の挙動を確認します。
+ $()関数を使います。

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>Kronos.js</title>
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js"></script>
  <script type="text/javascript">
  $(function() {
    $(".status").html("ready!");
  });
  </script>
</head>
<body>
  <h1>Sample 1</h1>
  <div class="status">kronos.js</div>
</body>
</html>
```

### sample2.html

イベントハンドラの作成方法を確認します。

+ $(".status").click(function(e){ /\* callback \*/ });

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>Kronos.js</title>
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js"></script>
  <script type="text/javascript">
  $(function() {
    $(".status").click(function(e){
      var fruits = ["apple", "banana", "cherry"];

      var $ul = $("<ul>");
      for (var i = 0; i < fruits.length; i++) {
        // $ul.append($("<li>").text(fruits[i]));
        var $li = $("<li>");
        $li.text(fruits[i]);
        $ul.append($li);
      }
      $(".status").append($ul);
    })
  });
  </script>
</head>
<body>
  <h1>Sample 2</h1>
  <div class="status">kronos.js</div>
</body>
</html>
```

### sample3.html

jQueryのアニメーションを確認します。

+ $(".status").fadeIn(3000);

> fadeOutなどもあります。

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>Kronos.js</title>
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js"></script>
  <script type="text/javascript">
  $(function() {
    $("#show-btn").click(function(){
      $(".status").fadeIn(3000);
    })
  });
  </script>
</head>
<body>
  <h1>Sample 3</h1>
  <button type="button" id="show-btn">show</button>
  <div class="status" style="display:none">kronos.js</div>
</body>
</html>

```

### sample4.html

jQueryでCSSを更新してみます。

+ $(".red").css("backgroundColor", "red").css("color", "#ddd");

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>Kronos.js</title>
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js"></script>
  <script type="text/javascript">
  $(function() {
    $("#show-btn").click(function(){
      $(".red").css("backgroundColor", "red").css("color", "#ddd");
      $(".yellow").css("backgroundColor", "yellow").css("color", "#666");
    })
  });
  </script>
</head>
<body>
  <h1 class="red">Sample 4</h1>
  <button type="button" id="show-btn">show</button>
  <ul>
    <li class="red">Apple</li>
    <li class="yellow">Banana</li>
    <li class="red">Cherry</li>
  </ul>
</body>
</html>
```


### sample5.html

Ajaxプログラムを作成します。このサンプルを実行するにはWebサーバ上に配置して、HTTP経由でアクセスする必要があります。

> ローカルにインストールされている任意のWebサーバで構いません。軽量のWebサーバ：Caddyがおすすめです。 https://caddyserver.com/


以下のテストデータをfruits.txtという名前で保存します。Webサーバの公開ディレクトリ下にapiディレクトリを作成し、apiディレクトリ直下に配置してください。

```
Apple,Banana,Cherry
```

> 通常、このようなAjaxで取得するデータはPHPなどのスクリプトで生成するのが一般的です。今回は静的なテキストファイルで動作確認をします。

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>Kronos.js</title>
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js"></script>
  <script type="text/javascript">
  $(function() {
    $("#show-btn").click(function(){
      $.ajax({
        url: "/api/fruits.txt",
        success: function(result) {
          $("#fruits-panel").text(result);
        },
      });
    })
  });
  </script>
</head>
<body>
  <h1 class="red">Sample 5</h1>
  <button type="button" id="show-btn">show</button>
  <div id="fruits-panel">kronos.js</div>
</body>
</html>
```


### sample6.html

JSONデータをやりとりするAjaxプログラムを作成します。このサンプルを実行するにはWebサーバ上に配置して、HTTP経由でアクセスする必要があります。

+ $.getJSON("/api/fruits.json")
+ .done()
+ .fail()

以下のテストデータをfruits.jsonという名前で保存します。Webサーバの公開ディレクトリ下にapiディレクトリを作成し、apiディレクトリ直下に配置してください。

```json
[
  {"id":1, "name":"Apple", "price": 100},
  {"id":2, "name":"Banana", "price": 200},
  {"id":3, "name":"Cherry", "price": 300}
]
```

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>Kronos.js</title>
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js"></script>
  <script type="text/javascript">
  $(function() {
    $("#show-btn").click(function(){
      $.getJSON("/api/fruits.json")
        .done(function(fruits){
          var $ul = $("<ul>");
          for (var i = 0; i < fruits.length; i++) {
            $ul.append($("<li>").text(fruits[i].name));
          }
          $("#fruits-panel").append($ul);
        }).fail(function(jqxhr, textStatus, error){
          var err = textStatus + ", " + error;
          console.log("Request Failed: " + err);
        });
    })
  });
  </script>
</head>
<body>
  <h1 class="red">Sample 6</h1>
  <button type="button" id="show-btn">show</button>
  <div id="fruits-panel">kronos.js</div>
</body>
</html>
```

> ulタグではなtableタグでフルーツのID、名前、価格を表示するように変更してみてください。
