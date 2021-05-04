# インターネット工学演習 10


## 概要

* webサーバの接続確認
* ネットワーク管理の基本コマンド



`

## WEBサーバの構築


## webサーバマシンにssh ログイン

#### R マシンがwebサーバ

```bash
192.168..0.27
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
cd /va	r/www/html

sudo mkdir 1811140000

sudo chown 1811140075a: 1811140075a 1811140075

cd 1811140075
```


## HTMLの作成

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


## コマンド

```bash
sudo tcpdump -Xvv -s 2048 -i eno1 rip
```


## digコマンド

* 特定のネームサーバに対してQUERYを発行する

```
$ dig A <domain> @<name server> 
```

```
dig A dns.joho.fuk.kindai.ac.jp @rs6000.cc.kindai.ac.jp
```
	
* IPアドレスからドメイン名を取得する（逆引き)

```
$ dig -x <ipaddress>
```

```
dig -x 157.13.61.6
dig -x 157.13.59.1
```

* ドメイン名に対応するMXレコードを取得する

```
$dig MX <domain>
dig MX fuk.kindai.ac.jp
```

* ルートDNSから確認を行う

```
$dig ドメイン名 +trace
```

* ルートDNSから確認を行う

```
$dig ネームサーバー soa
```

## apt-getを使ったインストール

```
sudo apt-get install パッケージ名

```

```
sudo apt-get -y install apache2 
```


### named (bind9) のインストール

```
sudo apt -y install bind9 bind9utils 

```

### bind9 の設定

* BINDのオプションを設定


/etc/bind/named.conf.options

```
sudo emacs  /etc/bind/named.conf.options
```

/etc/bind/named.conf.local 

```
sudo emacs /etc/bind/named.conf.local 
```

## ソースコードからのソフトのインストール方法

* (1)ソースコードを取得する

```
wget 　ファイルのURL 
```

* (2)圧縮されているソースコードを展開する

```
tar　コマンド
```

* (3)コンパイルの環境を整える

```
configure　スクリプト
```

* (4)コンパイルの実行

```
make コマンド
```

* (5)完成したバイナリコードをインストールする

```
sudo make install
```

## 圧縮ファイルの展開方法


* tar 形式（多数のファイルをまとめる）

	ファイルの形式が  .tar

	展開　tar xf ファイル名

* *gzip 形式　（サイズを圧縮して小さくする）

	ファイルの拡張子が　.gz 

	展開　gunzip ファイル名 

* bzip2形式（zipよりもさらにサイズが小さい）

	ファイルの拡張子が  .bz2

	展開　bunzip2 ファイル名

	tar でまとめて　gzip や bzip2で圧縮されている

*ファイルの拡張子が　　.tar.gz　　.tar.bz2

 展開　tar xfz ファイル名      tar xfj  ファイル名



