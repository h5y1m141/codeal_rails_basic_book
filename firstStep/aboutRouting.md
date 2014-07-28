## 最後にルーティングの概念説明

Webブラウザからのリクエストに対して、どの処理に情報を渡すか定義されており、これをルーティングと呼びます。ルーティングの情報からコントローラーとアクションが決定されるのですが、Webブラウザを起動して以下URLにアクセスしてみましょう

[http://localhost:3000/routes/info](http://localhost:3000/routes/info)

すると、以下の様な画面が表示されます。

![](../image/shot-2014-07-25-15.03.52.png)

上記の中で以下の記述の所をピックアップして説明します。

HTTP Verb |Path|	Controller#Action
---------|-----|-----------------------
GET | /tasks(.:format) | tasks#index


localhost:3000/tasks/

### ルーティングの定義はscaffoldで自動生成されるファイル内にて行われてる

このルーティングの定義をどこでやってるかというと 作成したプロジェクトの **config/routes.rb**にて行ってます。

このファイルを開くとコメントが多数記載されてますが、それを取り除いたものを記載すると

```ruby
Rails.application.routes.draw do
  resources :tasks
end
```
と、わずか3行の情報だけで、特に2行目の**resources :tasks** の記述がポイントになっています。

resourcesというメソッドに、:tasksを渡すことで、Webアプリケーションでよく行われる

- データの作成（Create）
- データの表示（Read）
- データの更新（Update）
- データの削除（Delete/Destory）

という操作（それぞれの英単語の頭文字をとってCRUDと言われます）のルーティングが設定されます。
