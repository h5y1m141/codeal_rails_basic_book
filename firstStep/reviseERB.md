## テンプレートエンジンとは？

特殊な記法を用いて、データベースから取得したデータを展開しててHTMLを生成するようなものを、テンプレートエンジンと呼びます。

Railsではいくつかのテンプレートエンジンに対応しており、主なものとおおまかな特徴を以下にまとめました。

テンプレートエンジンの名前 | 特徴
--------------------|----
ERB |Rubyで標準添付されてるテンプレートエンジンで、Railsでも標準のテンプレートエンジンとして採用されてます。
Haml | HTMLの構造をシンプルなインデントで表現したテンプレートエンジン。標準添付されてないですが、利用にあたっては、自分でインストールする必要があります
Slim | Haml同様にHTMLの構造をシンプルなインデントで表現したものですが、Hamlよりも、より簡潔な表現ができます

この講座では標準添付されてるERBを利用していきます。


## ERBを編集する

scaffoldを実行した際に、ERBベースのファイルがすでに生成されており、以下ディレクトリにあるファイルを編集していく形になります。

- /app/views/layoutsディレクトリ
    - application.html.erb
- /app/views/tasksディレクトリ
    - _form.html.erb
    - edit.html.erb
    - index.html.erb
    - new.html.erb
    - show.html.erb

/app/views/tasksディレクトリには、index.json.jbuilder と show.json.jbuilder というファイルもあるかと思いますが、今回の講座ではこのファイルは利用しないためこれは編集しなくてOKです



### /app/views/layouts/application.html.erb

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=Edge,chrome=1">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title><%= content_for?(:title) ? yield(:title) : "Todo" %></title>
    <%= csrf_meta_tags %>
    <!--[if lt IE 9]>
      <script src="//cdnjs.cloudflare.com/ajax/libs/html5shiv/3.6.1/html5shiv.js" type="text/javascript"></script>
    <![endif]-->
    <%= stylesheet_link_tag "application", :media => "all" %>
    <%= favicon_link_tag 'apple-touch-icon-144x144-precomposed.png', :rel => 'apple-touch-icon-precomposed', :type => 'image/png', :sizes => '144x144' %>

    <%= favicon_link_tag 'apple-touch-icon-114x114-precomposed.png', :rel => 'apple-touch-icon-precomposed', :type => 'image/png', :sizes => '114x114' %>
    <%= favicon_link_tag 'apple-touch-icon-72x72-precomposed.png', :rel => 'apple-touch-icon-precomposed', :type => 'image/png', :sizes => '72x72' %>
    <%= favicon_link_tag 'apple-touch-icon-precomposed.png', :rel => 'apple-touch-icon-precomposed', :type => 'image/png' %>
    <%= favicon_link_tag 'favicon.ico', :rel => 'shortcut icon' %>
    <%= javascript_include_tag "application" %>
  </head>
  <body>
    <!-- navigation bar -->
    <div class="navbar navbar-inverse navbar-fixed-top" role="navigation">
      <div class="container">
        <div class="navbar-header">
          <button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse">
            <span class="sr-only">Toggle navigation</span>
            <span class="icon-bar"></span>
            <span class="icon-bar"></span>
            <span class="icon-bar"></span>
          </button>
          <a class="navbar-brand" href="/tasks">RailsToDo</a>
        </div>
        <div class="collapse navbar-collapse">
          <ul class="nav navbar-nav">
            <li class="active"><a href="/tasks">Home</a></li>
            <li><%= link_to "タスク登録", "/tasks/new"  %></li>
          </ul>
        </div><!--/.nav-collapse -->
      </div>
    </div>
    <div class="wrapper">
      <!-- ここからメインとなる部分の表示。2カラムのレイアウトにしてます -->
      <div class="container-fluid">
        <div class="row-fluid">
          <div class="span12">
            <div class="row-fluid">
              <div class="span2"></div>
              <div class="span10">
                <%= yield %>
              </div>            
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="push"></div>
    <!-- footer -->
    <div class="footer-wrapper">
      <div class="navbar navbar-fixed-bottom">
        <div class="container">
          <footer>
            <h3>about Me</h3>
            <div class="row-fluid">
              <div class="span2">
                <div class="collapse navbar-collapse">
                  <ul class="nav navbar-nav">
                    <li>
                      <img src="<%= asset_path "facebook.png" %>" />
                    </li>
                    <li>
                      <img src="<%= asset_path "twitter_bird.png" %>" />
                    </li>
                  </ul>              
                </div>
              </div>
              <div class="span6"></div>
              <div class="span2"></div>
              <div class="span2"></div>
            </div>
          </footer>
        </div>
      </div>
	</div><!--/ここまでfooter wrapper -->
  </body>
</html>
```
### /app/views/tasks/index.html.erb

```html
<h2>タスク一覧</h2>
<div class="container-fluid">
  <div class="row-fluid">
    <div class="span12">
      <div class="container-fluid">
        <div class="row-fluid">
          <div class="span6">
            <table class="table table-striped">
              <tbody>
                <% @tasks.each do |task| %>
                <tr>
                  <td width="60%">
                    <%= task.content %>
                  </td>
                  <td>
                      <%= link_to '<button type="button" class="btn btn-primary"><i class="glyphicon glyphicon-info-sign"></i>　表示</button>'.html_safe, task %>
                    
                    <!-- <button type="button" class="btn btn-warning"> -->
                    <!--   <%= link_to 'Edit', edit_task_path(task) %> -->
                    <!-- </button> -->
                      <%= link_to '<button type="button" class="btn btn-danger"><i class="glyphicon glyphicon-remove-sign"></i>　削除</button>'.html_safe, task, method: :delete, data: { confirm: '本当に削除しますか?' } %>
                      <!-- <%= link_to '削除', task, method: :delete, data: { confirm: 'Are you sure?' } %> -->
                    </button>

                  </td>

                </tr>
                <% end %>
              </tbody>
            </table>
          </div>
        </div>
    </div>
</div>
```


### /app/views/tasks/show.html.erb

```html
<p id="notice"><%= notice %></p>

<div　class="container">
  <div class="row">
    <div class="col-sm-6 col-md-3">

      <article class="thumbnail">
        <img src="<%= asset_path "todo.jpg" %>" />
        <h3>タスク名： <%= @task.content %></h3>
        <p>
          <%= link_to '<button type="button" class="btn btn-primary"><i class="glyphicon glyphicon-edit"></i>　編集する</button>'.html_safe, edit_task_path(@task) %>

          <%= link_to '<button type="button" class="btn btn-danger">中止する</button>'.html_safe, tasks_path %>

        </p>

      </article>

    </div>
  </div>
</div>
```


### /app/views/tasks/_form.html.erb

```html
<div class="container-fluid">
  <div class="row-fluid">
    <div class="span12">
      <div class="row-fluid">
        <div class="span6">
          <%= form_for(@task) do |f| %>
          <% if @task.errors.any? %>
          <div id="error_explanation">
            <h2><%= pluralize(@task.errors.count, "error") %> prohibited this task from being saved:</h2>

            <ul>
              <% @task.errors.full_messages.each do |message| %>
              <li><%= message %></li>
              <% end %>
            </ul>
          </div>
          <% end %>

          <div class="field">

            <%= f.text_area :content , class: 'form-control', rows: '5' %>
          </div>
          <div class="actions">
            
            <% if request.path_info == "/tasks/new" then%>
              <%= f.submit "登録する" , class: 'btn  btn-primary' %>
              <%= link_to '<button type="button" class="btn btn-danger">中止する</button>'.html_safe, tasks_path %>

            <% else %>
              <%= link_to '<button type="button" class="btn btn-primary"><i class="glyphicon glyphicon-circle-arrow-left"></i>　一覧画面に戻る</button>'.html_safe, tasks_path %>
              <%= f.submit "更新する" , class: 'btn btn-danger' %>
            <% end %>
          </div>
          <% end %>

        </div>
      </div>
      
    </div>
  </div>
</div>
```

### /app/views/tasks/new.html.erb

```html
<h1>タスクを登録する</h1>

<%= render 'form' %>
```

### /app/views/tasks/edit.html.erb

```html
<h1>タスクを編集する</h1>

<%= render 'form' %>
```
