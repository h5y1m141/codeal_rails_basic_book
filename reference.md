## Vagrant＋Chefによる環境構築

### scaffoldを使ってひな形となるアプリを自動生成させる

```sh
./bin/rails g scaffold task content:text
```

実行結果

```sh
      invoke  active_record
      create    db/migrate/20140714042253_create_tasks.rb
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
vagrant@ubuntu-14:/vagrant/src/todo$
```

### db:migrateを実行する

```sh
./bin/rake db:migrate
```

```sh
== 20140714042253 CreateTasks: migrating ======================================
-- create_table(:tasks)
   -> 0.0066s
== 20140714042253 CreateTasks: migrated (0.0070s) =============================

```

画像の埋め込み


