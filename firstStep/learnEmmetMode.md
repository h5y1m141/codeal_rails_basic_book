## 効率的にコーディングするためにEmmetモードの機能を知る

先ほどの作業で、Emmetモードの準備が整ったので、効率的にコーディングするためにEmmetモードの機能について順番に解説します。

例えば、以下のようなベースとなるHTMLファイルを作成するとします

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8"/>
    <title>Document</title>
  </head>
  <body>
  </body>
</html>
```

これを、普通にコーディングするとなると、シフトキーを押しながら、< のキーをタイプして、その後、シフトキーを押しながら、!のキーを入力して・・・という感じでそれなりのキーをタイピングする必要があります。

Emmetモードを利用すると

```
html:5
```

とタイプして、コントロールキーを押しながら、**e** のキーを押すとhtml:5という部分が、以下のように変換されます。

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8"/>
    <title>Document</title>
  </head>
  <body>
  </body>
</html>
```

### Emmetモードの基本操作

1. コマンドを入力。先ほどの例だと、html:5 
2. Controlキー（以下、ctrl）を押しながら**e** のキーを押す

というのが基本操作になります。ユーザインタフェースのカスタマイズの場合には、すでに出来上がったものを修正するとはいえ、それなりにマークアップタグを入力しないければいなくなるため、こういう便利機能を積極的に利用しましょう。


## 実際にありそうな状況を想定して、Emmetモードを活用して効率的にコーディングする方法

実際にありそうな状況を想定して、Emmetモードを活用して効率的にコーディングする方法をいくつか紹介します。

### id属性のあるタグを入力する場合

例えばcontainerという名前のid属性が付与されてるdivタグを入力したい場合には以下のようにします。

1. div#containerと入力
2. ctrl キーを押しながら**e** のキーを押す
3. 展開されるHTMLはこのようになります

```html
<div id="container"></div>
```

### class属性のあるタグを入力する場合

例えばrow-fluidという名前のclass属性が付与されてるdivタグを入力したい場合には以下のようにします。

1. div.row-fluidと入力
2. ctrl キーを押しながら**e** のキーを押す
3. 展開されるHTMLはこのようになります


```html
<div class="row-fluid"></div>
```

### 複数のclass属性のあるタグを入力する場合

例えば、buttonというタグに、btnという名前のclass属性と、btn-primaryという名前のclass属性を付与したい場合には以下のようにします。

1. button.btn.btn-primaryと入力
2. ctrl キーを押しながら**e** のキーを押す
3. 展開されるHTMLはこのようになります


```html
<button class="btn btn-primary"></button>
```

### 入れ子のタグを入力する場合

例えばcontainerという名前のclass属性が付与されてるdivタグを入力。その中にrowという名前のclass属性が付与されてるdivタグを入力。さらに、その中に、col-sm-6とcol-md-3rowという複数のclass属性が付与されてるdivタグを入力したい場合には以下のようにします。

1. div.container>div.row>div.col-sm-6.col-sm3
2. ctrl キーを押しながら**e** のキーを押す
3. 展開されるHTMLはこのようになります

```html
<div class="container">
  <div class="row">
    <div class="col-sm-6 col-sm3"></div>
  </div>
</div>
```

ポイント：タグを入れ子にしたい場合には、**タグ名>タグ名** という形で、**>** を入れます。

### 複数のタグが繰り返されるときには、乗算の記号を組み合わせるとさらに効率的

例えばulタグにliを5個繰り返して入力するような場合には以下のようにします。

1. ul>li*5
2. ctrl キーを押しながら**e** のキーを押す
3. 展開されるHTMLはこのようになります

```html
<ul>
  <li></li>
  <li></li>
  <li></li>
  <li></li>
  <li></li>
</ul>
```

ポイント：繰り返しをする場合には、タグ名の後に、乗算を意味する***** を入力して、繰り返したい数値（今回の場合には5）を入力します。


## 最後に

今回の資料は、以下のスライドを参考にしながら記述していますので興味ある方は以下もご覧になることをおすすめします。

- はじめてのEmmet with Sublime Text2
    - URL: [http://www.slideshare.net/sada_h/emmet-with-sublime-text2](http://www.slideshare.net/sada_h/emmet-with-sublime-text2)
