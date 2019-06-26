# インターネット工学演習 11

## WEBサーバの構築2

## レポートURL

[https://forms.gle/ozTrGNggPfvw2gdu6
](https://forms.gle/ozTrGNggPfvw2gdu6
)

## aptによるapache2 のインストール

```bash
sudo apt install apache2
```

## apach2 のドキュメントルート

```bash
cd /var/www/html
```

### index.htmlを名称変更

```bash
sudo mv index.html index.homl.org
```

## index.htmlを作成する

```bash
sudo nano index.html
```

### 作成するHTML

自分の名前のページを作成する

```html
<html>
	<head>
		<meta charset="utf-8"/>
	</head>
	<body>
		<h1>山崎のページ</h1>
	</body>
</html>
```

### 自分のページにアクセスする

URL

	http://localhost/

### 隣の人のページを見る

各自のIPアドレスを知る

	http://IPアドレス/
	
## form 文を含むページ

自分のページを修正する

```bash
cd /var/www/html
nano index.html
```


```html
<html>
	<head>
		<meta charset="utf-8"/>
	</head>
	<body>
		<h1>あまぞん</h1>
		<form method='GET' action='cgi-bin/test.rb'>
		<p>商品</p>
		<input type='text' name='product'>
		<p>数量</p>
		<input type='text' name='amount'>
		<p>
		<input type='submit' name='注文'>
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

apache2 の設定ファイルのディレクトリに移動

```bash
cd /etc/apache2/conf-available
```

#### serve-cgi-bin.conf を編集

```bash
sudo nano /etc/apache2/conf-available/serve-cgi-bin.conf 
```

```
...
                <Directory "/usr/lib/cgi-bin">
                        Options +ExecCGI -MultiViews +SymLinksIfOwnerMatch
                        AddHandler cgi-script .cgi .rb
                        AllowOverride None
                        Require all granted
                </Directory>
...                
```

### apache2を再起動

```bash
sudo systemctl restart apache2
```

### スクリプトエイリアス用ディレクトリへ移動

```bash
cd /usr/lib/cgi-bin/
```

### CGIスクリプトの作成

Rubyで作成する

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
puts "<html>
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
curl http://localhost/cgi-bin/test.rb?product=ぽるしぇ&amount=100
```

