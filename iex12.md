# インターネット工学演習 12

# WEBサーバの構築2

## AWS educate

https://aws.amazon.com/jp/education/awseducate/

### ubuntu 20.04LTS のインスタンスを起動してSSH接続


## HTML作成


## form 文を含むページ

自分のページを修正する

```bash
sudo nano index.html
```

```html
<meta charset="UTF-8">
<html>
 <head>
 </head>
 <body>
  <h1>あまぞん”自分の名前”</h1>
  <form method='GET' action='/cgi-bin/test.rb'>
    <p>商品</p>
    <input type='text' name='product'>
    <p>数量</p>
    <input type='text' name='amount'>
    </p><p>
    <input type='submit' value='注文'>
    </p>
  </form>
	</body>
</html>
```

## CGI プログラムを動かす

## ruby のインストール

```bash
sudo apt install ruby
```


### apache2 にCGIとして実行できるようにする

```bash
sudo a2enmod cgid 
```

### apache2を再起動

```bash
sudo service apache2 restart
```


#### apache2 の設定ファイルのディレクトリ

```bash
cd /usr/lib/cgi-bin
```



### スクリプトエイリアス用ディレクトリへ移動してディレクトリの作成所有権変更

```bash
cd /usr/lib/cgi-bin/
```


### CGIスクリプトの作成


```bash
sudo nano test.rb
```

1行目のは#! は「シェバング」と呼ばれるもので、スクリプトを実行する言語処理系を呼び出すためのもの

```ruby
#!/usr/bin/env ruby
require 'cgi'
cgi=CGI.new

puts "Content-type: text/html"

puts "\n\n"

puts "
<html>
<head>
<meta charset='utf-8'/>
</head>
<body>
<h1>お買い上げありがとうございます</h1>
<p>明日の８時に#{cgi['product']}を#{cgi['amount']}個お届けします</p>
</body>
</html>
"
```

### スクリプトに実行権限を与える

```bash
sudo chmod a+x test.rb
```

### スクリプトのテスト（デバッグ）

CGIではなくコマンドとして実行してみる

```bash
./test.rb
```

入力待ち状態になれば成功

試しに入力も入れてみる

入力の終了は、^d (コントロールキー＋ｄ)

```
product=ぽるしぇ&amount=100
```

その結果、以下のようなHTMLが出力されれば成功

```html
<html>
<head>
<meta charset='utf-8'/>
</head>
<body>
<h1>お買い上げありがとうございます</h1>
<p>明日の８時にぽるしぇを100個お届けします</p>
</body>
</html>
```

http経由で実行してみる

```bash
sudo apt install curl
```

```bash
curl http://localhost/cgi-bin/test.rb?product=ぽるしぇ&amount=100
```


-----------------------


### http経由で実行してみる

curlコマンドのインストール

```bash
sudo apt install curl
```

curlコマンドで実行

```bash
curl http://＜IPアドレス＞/cgi-bin/test.rb?product=ぽるしぇ&amount=100
```

### ブラウザからやってみる

```
http://106.157.214.199/(自分の学籍番号)/index.html
```

### 例
	
```
http://106.157.214.199/18111400000/index.html
```


## RESTful Webアプリケーション

## Ruby インストール



## Railsインストール

### 事前にOS をupdate, upgradeしておく

```bash
sudo apt update
sudo apt -y upgrade
```

```bash
sudo apt install -y autoconf bison build-essential libssl-dev libyaml-dev libreadline-dev zlib1g-dev libncurses5-dev libffi-dev libgdbm-dev sqlite3 libsqlite3-dev
sudo apt install -y nodejs npm
sudo npm install n -g
sudo n stable
sudo apt purge -y nodejs npm
exec $SHELL -l
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt update
sudo apt install -y yarn
sudo apt install -y ruby ruby-dev
sudo apt install -y ruby-bundler

sudo gem install nokogiri
sudo gem install sqlite3
sudo gem install rails
```

## 最初のRailsアプリの作成

```bash
mkdir rails
cd rails
bundle install
rails new kindai

## パスワードを入れる

cd kindai

bundle install

rails g scaffold Blog title date:datetime text:text picture:string
rake db:migrate
rails webpacker:install

## ポート番号を指定して起動
rails s -b 0.0.0.0 -p ボート番号
```

ポートマッピング

* 192.168.0.27	:8001
* 192.168.0.35	:8002
* 192.168.0.66	:8003
* 192.168.0.227	:8004
* 192.168.0.34	:8005
* 192.168.0.130	:8006
* 192.168.0.162	:8007
* 192.168.0.33	:8008
* 192.168.0.194	:8009
* 192.168.0.226	:8010


###  トップページにアクセス

* IPアドレスをしらべる

URLにアクセス

```
 http://106.157.214.199:ポート番号/blogs
```

## RESTful APIの確認

### 新規作成
* New Blog をクリック
 * 情報を入れる
 * ページから情報を入れる
* create blog ボタン
* back

### （モデル名（英語）の複数形で一覧）

### 参照 識別ID

### 修正　識別ID

### 削除　識別ID



この手順でいくつか記事を作成／削除する

### 新たなターミナルでRailsのディレクトリにアクセスする

* rails ルートディレクトリ

```bash
cd ~
cd rails
cd kindai
```
 
###  Bootstrap でデザインを追加
 
 * application.html.erbを編集

 ```bash
 nano app/views/layouts/application.html.erb
 ```
 
 以下のように修正
 
 ```heml
<!DOCTYPE html>
<html>
  <head>
    <title>Kindai</title>
    <%= csrf_meta_tags %>
    <%= csp_meta_tag %>
    <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css">
    <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap-theme.min.$
    <%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_pack_tag 'application', 'data-turbolinks-track': 'reload' %>
  </head>

  <body>
    <div class="container">
      <%= yield %>
    </div>

  <footer>
  <div class="container">Kindai 2019 </div>
  </footer>
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
  <script src="//maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js"></script>
  </body>
</html>
 ```
 
  
#### CSSを修正
 
```bash
nano app/assets/stylesheets/application.css
```
 
 ファイルの最後に以下を追加
 
```css
body { padding-top: 100px; }
footer { margin-top: 100px; }
table, td, th { vertical-align: middle; border: none; }
th { border-bottom: 1px solid #DDD; }
```
 
### 写真アップロード機能を追加
 
 rails root の Gemfile を修正
 
 ```bash
 nano Gemfile
 ```

次の一行を追加

```ruby
gem 'carrierwave'
```

 bundler を実行
 
 ```bash
 bundle install
 ```
 
 ### 写真アップローダのジェネレータの実行
 
 ```bash
 rails generate uploader Picture
 ```

### モデルの修正

```bash
nano app/models/blog.rb
```

```ruby
class Blog < ApplicationRecord
  mount_uploader :picture, PictureUploader
end
```

### formの修正

```bash
nano app/views/blogs/_form.html.erb
```

修正した結果

```html
<%= form_with(model: blog, local: true) do |form| %>
  <% if blog.errors.any? %>
    <div id="error_explanation">
      <h2><%= pluralize(blog.errors.count, "error") %> prohibited this blog from being saved:</h2>

      <ul>
        <% blog.errors.full_messages.each do |message| %>
          <li><%= message %></li>
        <% end %>
      </ul>
    </div>
  <% end %>

  <div class="field">
    <%= form.label :title %>
    <%= form.text_field :title %>
  </div>

  <div class="field">
    <%= form.label :date %>
    <%= form.datetime_select :date %>
  </div>

  <div class="field">
    <%= form.label :text %>
    <%= form.text_area :text %>
  </div>

  <div class="field">
    <%= form.label :picture %>
    <%= form.file_field :picture %>
  </div>

  <div class="actions">
    <%= form.submit %>
  </div>
<% end %>


```

### ビューを修正

```bash
nano app/views/blogs/show.html.erb
```
修正部分

```ruby
<%= @blog.picture %>
```

修正結果

```ruby
<%= image_tag(@blog.picture_url, width: 600) if @blog.picture.present? %>
```

## RESTful APIの確認
