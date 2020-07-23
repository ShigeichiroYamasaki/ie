# インターネット工学演習 12

## web技術2

```ssh
ssh ユーザID＠106.157.214.199
```

### グループ

★リーダが欠席の場合：（１）先頭から循環順序で決定（２）２回以上している場合は次の人に

* がついている人が、班の中の今日のリーダです
* 毎回の授業で、リーダの人が代表して sudo コマンドを実行します
* リーダー以外の人がsudo コマンドを実行してはいけません。

```
1班

L 1611140053
1811140016
1811140051
1811140031
1811140025
1811140077

２班

L 1811140075
1811140063
1611140017
1811140045
1811140057
1811140020

３班

L 1811140007
1811140058
1611140076
1811140036
1811140010
1811140024

４班

L 1811140054
1811140070
1811140040
1811140053
1811140038
1811140068

５班

L 1611140051
1811140080
2011141001
1811140033
1811140030
1811140067

６班

L 1711140059
1811140052
1811140032
1811140079
1811140023
1811140008

７班

L 1711140016
1811140012
1811140061
1811140022
1811140002
1811140078

８班

L 1811140042
1811140044
1811140015
1811140017a
1811140066
1811140001

９班

L 1711140049
1811140029
1811140019
1811140011
1811140037
1811140050

10班

L 1811140064
1811140071
1811140034
1811140003
1811140073
1811140014
```



## 先週にやったことの確認


### webサーバマシンにssh ログイン

#### R マシンがwebサーバ

```bash
ssh ユーザID@192.168.0.27
```

## 自分のhtml用ディレクトリを作成

```bash
cd /var/www/html

sudo mkdir ディレクトリ名（自分の学籍番号にしてください）
sudo chown 自分のアカウント:自分のアカウント ディレクトリ名

cd ディレクトリ名
```

実行例

```bash
cd /var/www/html

sudo mkdir 18111400000
sudo chown  s18111400000r:s18111400000r 18111400000 

cd 18111400000
```


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
  <h1>あまぞん</h1>
  <form method='GET' action='/cgi-bin/(自分の学籍番号)/test.rb'>
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

## ブラウザでURLでアクセスする

```
http://106.157.214.199/(自分の学籍番号)/index.html
```

### 例
	
```
http://106.157.214.199/18111400000/index.html
```

## CGI プログラムを動かす

### apache2にcgiモジュールを組み込む

```bash
sudo a2enmod cgi
```

### apache2 に.rb ファイルをCGIとして実行できるように設定する

#### apache2 の設定ファイルのディレクトリ

```bash
cd /etc/apache2/conf-available
```


-----------------------

## 今週


### スクリプトエイリアス用ディレクトリへ移動してディレクトリの作成所有権変更

```bash
cd /usr/lib/cgi-bin/

sudo mkdir（自分の学籍番号または名前)

sudo chown ユーザID:ユーザID （自分の学籍番号または名前)

cd （自分の学籍番号または名前)
```

実行例

```bash
cd /usr/lib/cgi-bin/

sudo mkdir 18111400000
sudo chown  s18111400000r:s18111400000r 18111400000 

cd 18111400000
```


### CGIスクリプトの作成


```bash
nano test.rb
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
chmod a+x test.rb
```

### スクリプトのテスト（デバッグ）

CGIではなくコマンドとして実行してみる

```bash
./test.rb
```

* 入力待ち状態になれば成功

#### 試しに入力も入れてみる

* 入力の終了は、^d (コントロールキー＋ｄ)

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

#### http経由で実行してみる

curlコマンドのインストール

```bash
sudo apt install curl
```

curlコマンドで実行

```bash
curl http://106.157.214.199/cgi-bin/(学籍番号)/test.rb?product=ぽるしぇ&amount=100
```

例

```bash
curl http://106.157.214.199/cgi-bin/18111400000/test.rb?product=ぽるしぇ&amount=100
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


## ネットワーク構成

```
                                     Internet
                                 <106.157.214.199>
                                     [ルータ]
                                         |
      26                 27              1           (192.168.0.X)
    ---+------------------+--------------+----------- 192.168.0.0/27
     [ T ](SSH)         [ R ]
                          |
  33      34      35      36                         (192.168.0.X)
--+-------+-------+-------+-------------------------- 192.168.0.32/27
[ C0]   [ B0]   [ A0] 
  |       |       |
  |       |      65     66                            (192.168.0.X)
  |       |      -+------+---------------------------- 192.168.0.64/27
  |       |            [ A1]  
  |       |              |               
  |       |             97                            (192.168.0.X)
  |       |             -+---------------------------- 192.168.0.96/28
  |       |                   
  |       |   
  |       |   
  |       |   
  |       |   
  |       |                     
  |     129    130                                    (192.168.0.X)
  |      -+------+------------------------------------ 192.168.0.128/27
  |            [ B1]  
  |              |
  |            161     162                            (192.168.0.X)
  |             -+-------+---------------------------- 192.168.0.160/28
  |                    [ B2]
  |                      |
  |                    177     178                    (192.168.0.X)
  |               -------+-------+-------------------- 192.168.0.176/28
  |                            [ B3]
  |                    
193    194                                            (192.168.0.X)
 -+------+-------------------------------------------- 192.168.0.192/27
       [ C1] 
         |
       225         226       227                      (192.168.0.X)
        -+-----------+---------+---------------------- 192.168.0.224/28
                   [ C2]     [ A2] 
                     |         |
                     |         |
                     |         |
                     |       113       114          ★(192.168.0.X)
                     |        -+---------+----------★ 192.168.0.112/28
                     |                 [ A3] 
                     |
                   241      242                       (192.168.0.X)
                    -+-------+------------------------ 192.168.0.240/28
                           [ C3]

```

## 担当ルータ(マシン）


| R    | A0   | A1   | A2   | B0   | B1   | B2   | C0   | C1   | C2   |
| :--- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 9班  |10班 | 1班  | 2班  | 3班  | 4班  | 5班  | 6班  | 7班  | 8班 |


### ポートマッピング

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


## 自分の班のマシンに移動

```
ssh ユーザID@IPアドレス
```

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
