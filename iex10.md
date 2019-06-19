# インターネット工学演習 10

## WEBサーバの構築

## レポートURL

[https://forms.gle/K9n1nzYbuE52gVmTA
](https://forms.gle/K9n1nzYbuE52gVmTA
)


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

## apt-getを使ったインストール

```
sudo apt-get install パッケージ名

```

```
sudo apt-get -y install apache2 
```


