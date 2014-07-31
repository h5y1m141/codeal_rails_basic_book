## Modelの内容を書き換えてみる

自動生成されたapp/models/task.rbは

```ruby
class Task < ActiveRecord::Base
end
```
となっており、class Task の後の **< ActiveRecord::Base** という記述があることで、Modelとしての処理が行えるようになってます。

そこで、試しに

```ruby
class Task
end
```

と書き換えて、Railsのconsole機能を一度終了して、再度console機能を立ち上げて、

```sh
task = Task.all
```

と入力してみましょう。おそらく

```sh
irb(main):001:0> task = Task.all
NoMethodError: undefined method `all' for Task:Class
        from (irb):1
```

というような形のエラーが表示されるかと思います。

このようにclass Task の後の **< ActiveRecord::Base** という記述が大事であり、この記述があることで、前述したデータベースと接続して、項目情報を取得した上で自動的に処理が行えるようになってます。

## 入力内容を確認する処理を加える

現在の作りだと、例えば、タスク登録をする際に、何も入力されていなくてもエラーにならずにそのまま登録できてしまいます。
