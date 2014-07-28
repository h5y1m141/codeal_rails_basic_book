## 一覧画面を表示する処理を書き換えてみましょう

app/controllers/tasks_controller.rbの先頭の6行目に、**def index** という記述があるかと思います。

```ruby
class TasksController < ApplicationController
  before_action :set_task, only: [:show, :edit, :update, :destroy]
  def index
    @tasks = Task.all
  end
  # 以下省略
end
```

この部分の処理が実際に一覧画面の処理に関わってきますので以下に処理内容を簡単に説明します

- Task.allという処理で、Taskというモデルを通じて、DB上のtasks テーブルのデータをすべて読み込む処理が行われます
- 読み込まれたファイルは@tasksという変数に格納されます
- テンプレートとなるファイルの選択を本来はこの後に行われるのですが、Railsの便利な仕組みがあるため、以下の命名規則から自動的に選択されます
    - app/views配下にあるディレクトリ名がController名と同じもの（今回の場合だとapp/views/tasksが参照される）の中にあるファイル名がアクション名と同じもの（今回の場合だとindexというものに該当します）が選択されます。結果として、**app/views/tasks/index.html.erb** に処理が移ります。

### 自動ではなく手動で処理をする

Railsの便利な仕組みがあるため、index の処理の最後では自動的にテンプレートエンジンが選択されました。

この省略されてる処理を自分で書くには以下のようにします

```ruby
class TasksController < ApplicationController
  before_action :set_task, only: [:show, :edit, :update, :destroy]
  def index
    @tasks = Task.all
    # 以下を追加
    render :action => "index"
  end
  # 以下省略
end
```

```sh
render :action => "アクション名"
```

という形で記述することで、アクション名に指定される処理（今回の場合はindex）に処理が移ります。

また、render のオプションは

```sh
render :template => "コントローラ名/アクション名"
```

という書き方も出来ます。そのため

```ruby
class TasksController < ApplicationController
  before_action :set_task, only: [:show, :edit, :update, :destroy]
  def index
    @tasks = Task.all
    # 以下を追加
    render :template => "tasks/index"
  end
  # 以下省略
end
```

の方が、今回についてはより理解しやすい書き方になるかと思います。

### 表示形式をJSON形式にする

今回のようなサンプルアプリの場合には正直あまり使い道無いのですが、表示形式をHTMLではなく、JSON形式にすることもできます。

```ruby
class TasksController < ApplicationController
  before_action :set_task, only: [:show, :edit, :update, :destroy]
  def index
    @tasks = Task.all
    # 以下を追加
    render :json => @tasks
  end
  # 以下省略
end
```
