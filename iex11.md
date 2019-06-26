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
	<head></head>
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


```hrml
<html>
	<head></head>
	<body>
		<h1>山崎のページ</h1>
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

## CGI プログラム

スクリプトエイリアスへ移動

