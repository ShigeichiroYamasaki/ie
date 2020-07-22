# インターネット工学演習 13
## RESTful Webアプリケーション

## Railsインストール

### 事前にOS をupdate, upgradeしておく

```bash
sudo apt update
sudo apt upgrade
```

```bash
sudo apt install autoconf bison build-essential libssl-dev libyaml-dev libreadline-dev zlib1g-dev libncurses5-dev libffi-dev libgdbm-dev sqlite3 libsqlite3-dev
sudo apt install -y nodejs npm
sudo npm install n -g
sudo n stable
sudo apt purge -y nodejs npm
exec $SHELL -l
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt-get update
sudo apt-get install yarn

sudo gem install sqlite3
sudo gem install rails
```

## 最初のRailsアプリの作成

```bash
mkdir rails
cd rails
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

###  トップページにアクセス

* IPアドレスをしらべる

URLにアクセス

```
 http://106.157.214.199:ポート番号/blogs
```

* New Blog をクリック
* 情報を入れる
* ページから情報を入れる
* create blog ボタン
* back

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
 
 以下の行を見つける
 
 ```heml
 <%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track': 'reload' %>
 ```
 
 この行の前に次の行を追加する
 
 ```html
 <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css">
<link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap-theme.min.css">
 ```
 
 さらに
 
 ```html
   <body>
    <%= yield %>
  </body>
 ```
 
 の部分を以下のように書き換えます
 
 ```html
   <body>
   <div class="container">
    <%= yield %>
    </div>
  </body>
 ```
 
 #### ブラウザでデザインの変化を見てみる
 
 #### さらに</body>　の直前にナビゲーションを追加する
 
 ```html
 <footer>
  <div class="container">
Kindai 2019
  </div>
</footer>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
<script src="//maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js"></script>

</body>　
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
 bundle
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

修正する元

```html
<%= form.text_field :picture %>
```

修正した結果

```html
<%= form.file_field :picture %>
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
