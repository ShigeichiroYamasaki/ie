# インターネット工学演習 11


# WEBサーバの構築


## AWS educate

https://aws.amazon.com/jp/education/awseducate/

### ubuntu 20.04LTS のインスタンスを起動してSSH接続

## nginx のアンインストール

nginx でfastCGIを利用する方法は少し複雑なので，aapche2 を利用することにします。

* nginxサーバの停止

```bash
sudo service nginx stop
```

* apt でインストールしたパッケージをアンインストールする

```bash
sudo apt remove nginx
```

## apache2 のインストール

```bash
sudo apt install apache2
```


* apache2 の起動

```bash
sudo service apache2 start
```


## 自分のページの作成


```bash
cd /var/www/html

sudo nano index.html
```

## HTML

```html
<meta charset="UTF-8">
<html>
<head>
</head>
<body>
<h1>”自分の名前”のページ</h1>

</body>
</html>

```

## ブラウザでURLでアクセスする

```
http://グローバルアドレス/index.html
```


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

