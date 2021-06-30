# インターネット工学演習 13

# WEBアプリケーション3


## Ruby インストール

### snap 版Rubyのアンインストール

```bash
sudo snap remove ruby
```

### apt でRubyをインストール

```bash
sudo apt install ruby
```


### Ruby バージョンの確認

```
ruby -v
```


## CGI プログラムを動かす


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
http://＜IPアドレス＞/index.html
```


## RESTful Webアプリケーション



## Railsインストール

```bash
cd ~

nano install_rails.sh
```

```bash
#!/bin/bash
sudo apt update
sudo apt upgrade -y
sudo apt install -y build-essential 
sudo apt install -y clang
sudo apt install -y cmake
sudo apt install -y direnv
sudo apt install -y git
sudo apt install -y nodejs
sudo apt install -y ruby-dev
sudo apt install -y curl
sudo apt install -y imagemagick
sudo apt install -y yarn
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt update

sudo apt install -y sqlite3 libsqlite3-dev
sudo apt install -y npm
sudo npm install n -g
sudo n stable

sudo npm install -g npm
sudo npm install -g yarn

sudo gem install bundler
sudo gem install sqlite3
sudo gem install json-jwt
sudo gem install jwt
sudo gem install rails
sudo gem install twitter
sudo gem install devise
sudo gem install omniauth
sudo gem install omniauth-twitter
sudo gem install omniauth-facebook
```


### 実行

```bash
chmod u+x install_rails.sh

./install_rails.sh

sudo gem update
```

シェルの再起動

```bash
exec $SHELL -l
```

### Railsのテスト

```bash
rails new test1

cd test1

bundle install
```

#### scaffold で生成

```bash
rails g scaffold Blog title body:text
```

#### webpackerのインストール

```bash
rails webpacker:install
```



```bash
bundle install
```

### DB のマイグレーション

```bash
rails db:migrate
```


### サーバーの起動

```bash
rails s -b 0.0.0.0
```


## セキュリティグループを修正

* 自分のインスタンスのセキュリティグループ名を確認する　（launch-wizard-２など）
* セキュリティグループのタブを選択
* 自分のセキュリティグループのチェックボックスをチェックする
* 「インバウンドルール」のタブを選択
* 「インバウンドルールを編集」
* 「ルールを追加」
* TCP 3000 ポートを追加　ソースは 0.0.0.0/0
*


### ブラウザから確認

http://＜グローバルアドレス＞:3000/blogs

確認後，control-c でサーバを停止




## RESTful APIの確認

### 新規作成
* New Blog をクリック
 * 情報を入れる
 * ページから情報を入れる
* create blog ボタン
* back

### 一覧

|HTTP メソッド|	パス |目的|
|:--           |:--| :--| :--|
|GET 	|/blogs| 		一覧を表示|
|GET |/blogs/new| 作成するためのフォームを返す|
|POST |/blogs 	| 	作成する|
|GET |/blogs/:id| 	特定のオブジェクトを表示する|
|GET |	/blogs/:id/edit|編集用のフォームを返す|
|PATCH/PUT|/blogs/:id|特定のオブジェクトを更新する|
|DELETE|/blogs/:id|	特定のオブジェクトを削除する|


### curl コマンドでアクセスする



## 一般のwebアプリケーションのURLとRESTful API を確認

* google classroom API

https://developers.google.com/classroom/reference/rest

* twitter API

https://developer.twitter.com/en/docs/api-reference-index#twitter-api-v2














