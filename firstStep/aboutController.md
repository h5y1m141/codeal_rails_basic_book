## Controllerの役割

scaffoldで自動生成されるファイルがいくつかあり、先ほど編集していただいたERB以外にも重要なファイルがあり、その１つがControllerです。

Controllerの動きを理解するためには、Webブラウザからアプリケーションにアクセスした時の処理の流れを追うと理解が進むと思うので、自動的に生成されるファイルを一部カスタマイズしながら、処理内容をみてみましょう

## scaffoldで自動生成されたcontroller

scaffoldで自動生成された/app/controllers/tasks_controller.rbファイルでは以下7つの処理が定義されてます。

メソッド名 | 処理内容
--------|-------
index| 一覧画面を表示する
show|詳細表示画面を表示する
new|新規登録画面を表示する
edit|編集画面を表示する
create|新規登録処理をして詳細画面を表示する
update|更新処理をして詳細画面を表示する
destroy|削除処理をして一覧画面を表示する


app/controllers/tasks_controller.rbを開くと

```ruby
class TasksController < ApplicationController
  before_action :set_task, only: [:show, :edit, :update, :destroy]
  # 以下省略
end
```

となってるかと思いますが、一部の処理を実際に書き換えながら処理内容を理解しましょう。


