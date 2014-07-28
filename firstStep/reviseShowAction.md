## 詳細表示画面を表示する処理について

今度は、詳細表示画面を表示する処理についてみてみましょう。まずは自動的に生成されるコードは以下になります。

```ruby
class TasksController < ApplicationController
  before_action :set_task, only: [:show, :edit, :update, :destroy]
  # 一部省略
  def show
  end
  
  # 以下省略
end
```

### データベースの検索処理をどこで実行してるのか？

indexの時には Task.allという処理で、Taskというモデルを通じて、DB上のtasks テーブルのデータをすべて読み込む処理が行われていたのですが、今回のshowではそのような処理が行われていませんが、実際には画面上に詳細情報が表示されます。

詳細情報の取得処理をどこで行ってるかというと実は先頭の

```ruby
class TasksController < ApplicationController
  before_action :set_task, only: [:show, :edit, :update, :destroy]
```

の **before_action :set_task, only: [:show, :edit, :update, :destroy]** がポイントになります。

show,edit,update,destroyはそれぞれ処理内容が異なるのですが、**詳細画面を表示する** という部分においては共通した処理があります。

それぞれ共通した処理を切り出す（今回の場合にはset_taskというメソッド）ことで、show,edit,update,destroyといった個々の処理が行われる前に自動的に共通処理である set_taskが実施されます。

なお、set_taskの中身は

```ruby
class TasksController < ApplicationController
  # 一部省略
  private
    # Use callbacks to share common setup or constraints between actions.
    def set_task
      @task = Task.find(params[:id])
    end
end
```

という形でTasksControllerの後半で定義されており処理内容は以下のようになります。

- Task.findという処理で、Taskというモデルを通じて引数に渡されるidの値（上記のコードの **params[:id]** の箇所）を検索条件として、DB上のtasks テーブルのデータを検索します。
- 検索結果は、変数@taskに格納されます。


**def show** と **end** の間には何も書かれませんが、先ほどのindexの時同様に、Railsの便利な仕組みがあるため、**app/views/tasks/show.html.erb** に処理が移ります。

### indexの時と同様に自動ではなく手動で処理をする

試しに、showの所で行われる処理で、before_actionで定義されてる処理を一旦無効にして、showの中にすべてを記述すると以下のように書けるので試してみましょう

```ruby
class TasksController < ApplicationController
  # 以下をコメントアウトする
  # before_action :set_task, only: [:show, :edit, :update, :destroy]
  # 以下省略
  
  def show
    @task = Task.find(params[:id])
    render :action => "show"
  end
  # 以下省略
end
```

上記書き換えたら[http://localhost:3000/tasks/1](http://localhost:3000/tasks/1)にアクセスして実際に表示されることを確認してみましょう。

また、上記が確認できたら、HTMLではなくJSON形式で表示するために以下のように記述してみましょう

```ruby
class TasksController < ApplicationController
  # 以下をコメントアウトする
  # before_action :set_task, only: [:show, :edit, :update, :destroy]
  # 以下省略
  
  def show
    @task = Task.find(params[:id])
    render :json => @task
  end
  # 以下省略
end
```
