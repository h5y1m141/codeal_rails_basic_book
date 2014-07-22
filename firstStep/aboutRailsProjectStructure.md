## Railsのプロジェクトの構造を理解する

scaffoldを使うことで、Railsベースのアプリ開発が効率的に行えることが出来ますが、Railsのプロジェクトの構造について少し掘り下げて解説します。

## scaffoldで自動的に生成されるファイルで当面抑えておくべきファイルについて

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



