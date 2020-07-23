# インターネット工学演習 11


# WEBサーバの構築

### sshサーバにログイン

power shell などで ssh コマンド

```
ssh ユーザID@106.157.214.199
```


### webサーバマシンにssh ログイン

#### R マシンがwebサーバ

```bash
192.168.0.27
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

## 自分のページの作成

```bash
nano index.html
```


## HTML

```html
<meta charset="UTF-8">
<html>
<head>
</head>
<body>
<h1>自分の名前</h1>

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

## form 文を含むページ

自分のページを修正する

```bash
cd /var/www/html/(自分の学籍番号)/
sudo nano index.html
```

(自分の学籍番号)/

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


### apache2を再起動

```bash
sudo systemctl restart apache2
```

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

