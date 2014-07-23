## アプリのひな形を作る便利機能のscaffoldの紹介

Railsが提供する機能は多数ありますが、データの更新・削除やユーザインタフェースとなる部分のテンプレートといったアプリに必要な機能をひと通り生成してくれるscaffoldがあります。

この機能を使ってToDoアプリのひな形を実際に作ってみましょう。

## ToDoアプリの概要

ここでToDoアプリのシステム的な構造について少し掘り下げて解説しておきます。

### ToDoをTaskというモデルで表現する

１つのToDoを ** Task** という単位で操作することにし、このTaskをモデル名とします。先程少し触れましたが、モデル名は英単語で単数形で表現し、データベースの項目のテーブル名は英単語の複数形で表現するルールがRailsにはあるため以下の様な形になります

- モデル名：Task
- データベースのテーブル名：tasks
    - カラム名：content
    - 型：text
    - 概要：タスクの内容


## 実際にscaffoldを利用してみる

では早速scaffoldでアプリ開発に必要なファイルを作ってみましょう。

まずはターミナルを起動して、以下のコマンドを入力します。なお以下コマンドは、**先頭に ドット(.)** が入ってるので注意してください

```sh
./bin/rails generate scaffold task content:text
```

上記コマンドを実行すると、以下の様にたくさんのファイルが自動的に生成されます。

![](../image/terminal01.gif)

### DBの設定を行いまずはサンプルアプリが起動するまで確認する

出来上がるファイルのそれぞれの解説は後述しますので、まずは最低限の設定を行いサンプルアプリが起動するか確認します。

まずは以下コマンドを実行してデータベースの作成を行います。

```sh
./bin/rake db:create
```

その後、以下コマンドを入力します。

```sh
./bin/rake db:migrate
```

コマンドを入力すると、このような画面が表示されるかと思います。

![](../image/shot-2014-07-22-8.07.03.png)

その後、Railsで作ったアプリケーションを起動させるために以下コマンドを入力します。

```sh
./bin/rails server
```

以下のような画面が表示されて、一番最後の行に **WEBrick::HTTPServer#start** という文字が表示されていればOKです。

![](../image/shot-2014-07-22-8.40.41.png)

この状態が確認できたら、Webブラウザを起動します。

そして、

```sh
http://localhost:3000/tasks
```

にアクセスして、以下の様な画面が表示されることを確認します。

![](../image/shot-2014-07-22-8.41.11.png)

### サンプルアプリの動作を確認する

ここまでの作業が完了すると、データの登録、表示、削除といった基本的な操作が行えるようなアプリケーションが完成していますので試しに、データを１つ登録してみましょう

この画面のNew Task のリンクをクリックします

![](../image/shot-2014-07-22-8.41.11.png)

クリックすると、このような画面が表示されます。Content の項目に好きな文字を入力して、Create Taskボタンをクリックします

![](../image/shot-2014-07-22-8.41.30.png)

クリックするとこのような画面が表示されます。

![](../image/shot-2014-07-22-8.41.43.png)

### 過去に古いバージョンのRailsを触ったことがある方向けに、railsコマンドについて補足

Railsが提供する **rails** のコマンドを利用する際に、１つ前のバージョンの bundel exec rails... とせず、この講座では、bin ディレクトリに作成される **rails** スクリプトを実行します。

scaffoldを使うことで、Railsベースのアプリ開発が効率的に行えることが出来ますが、Railsのプロジェクトの構造について少し掘り下げて解説します。

### scaffoldで自動的に生成されるファイルで当面抑えておくべきファイルについて

さきほど、scaffold のコマンドを入力した際に以下のようにファイルが自動生成されました。

```sh
./bin/rails generate scaffold task content:text
      invoke  active_record
      create    db/migrate/20140720233458_create_tasks.rb
      create    app/models/task.rb
      invoke    test_unit
      create      test/models/task_test.rb
      create      test/fixtures/tasks.yml
      invoke  resource_route
       route    resources :tasks
      invoke  scaffold_controller
      create    app/controllers/tasks_controller.rb
      invoke    erb
      create      app/views/tasks
      create      app/views/tasks/index.html.erb
      create      app/views/tasks/edit.html.erb
      create      app/views/tasks/show.html.erb
      create      app/views/tasks/new.html.erb
      create      app/views/tasks/_form.html.erb
      invoke    test_unit
      create      test/controllers/tasks_controller_test.rb
      invoke    helper
      create      app/helpers/tasks_helper.rb
      invoke      test_unit
      create        test/helpers/tasks_helper_test.rb
      invoke    jbuilder
      create      app/views/tasks/index.json.jbuilder
      create      app/views/tasks/show.json.jbuilder
      invoke  assets
      invoke    coffee
      create      app/assets/javascripts/tasks.js.coffee
      invoke    scss
      create      app/assets/stylesheets/tasks.css.scss
      invoke  scss
      create    app/assets/stylesheets/scaffolds.css.scss
```

生成されるファイルの中で当面の開発で理解しておくべきファイル、ならびに、ディレクトリについてピックアップしておきます


- **app** ディレクトリ → **model** ディレクトリ の **task.rb** というファイル
- **app** ディレクトリ → **views** ディレクトリ → **taks** ディレクトリ の **拡張子がerb** というファイル
- **app** ディレクトリ → **controllers** ディレクトリ の **tasks_controller.rb** というファイル
- **app** ディレクトリ → **assets** ディレクトリ の **stylesheets** というディレクトリ
- **db** ディレクトリ → **migrate** ディレクトリ の **20140720233458_create_tasks.rb** というファイル。（ファイル名は各自の環境によって異なりますがその点は後述します）

Railsでの開発を始めた頃はapp ディレクトリ以下のファイルや、ディレクトリをよく参照することが多くなります。業務でRailsを使ったアプリケーションを開発するようになると、それ以外のファイル/ディレクトリも参照することが増えてきますが、まずは上記にピックアップした所がメインになってきますのでその点だけは覚えておいてください。

### app/model/以下

データベースとの接続とデータに対する操作、およびビジネスロジックを担うファイルがここに格納されます

### app/views/以下

Modelの内容を参照し、ユーザインタフェースを生成する役割を担うファイルがここに格納されます

### app/controllers/以下

ModelとViewをつなぐ役割を担うファイルがここに格納されます


### app/assets/以下

Viewのファイルの中で参照されるスタイルシート（CSS）のファイルや、JavaScriptのファイルなどがここに格納されます。なお、Railsでは、CSSやJavaScriptのファイルを効率的に書くことが出来る言語を採用しており、それぞれ

- SCSS → CSS
- CoffeeScript → JavaScript

という形になります。なおこの講座では、SCSS、CoffeeScriptについてはとりあげません。

### db/migration以下

データベースに対する操作は通常SQLという言語を利用して行うのですが、Railsの場合には、SQLを書かなくても操作が行える仕組みが整っており、そのためのファイルがscaffoldでdb/migration以下に自動的に生成されます

生成されたファイルを開いてみましょう。

```ruby
class CreateTasks < ActiveRecord::Migration
  def change
    create_table :tasks do |t|
      t.text :content

      t.timestamps
    end
  end
end
```

#### 処理内容の解説

このファイルの3行目のcreate_table()という処理でデータベース上にテーブルを作成する処理が行われてます。

また、scaffoldを行った際に

```sh
./bin/rails generate scaffold task content:text
```

としたかと思いますが、上記のmigrationファイルの4行目の **t.text :content** という記述の箇所がそれにあたります。

6行目の部分はscaffoldを実行した時に、Rails側で自動的に追加してる記述で、この記述があることで、データベースのtasksというテーブルに

- タスクの作成日を示すcreated_at という項目
- タスクの更新日を示す updated_at という項目

の２つが自動的に設定されます。

なお、ファイル名につく数値は日付や時刻などで、複数名で開発する際に重複しないように、ユニーク（一意）になり得るものが付与されてます。
