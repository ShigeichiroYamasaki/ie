# インターネット工学演習 10


## 概要

* RIPによる動的ルーティングの続き
	* 新しいネットワークでの自分のルータのルーティングテーブルを作成する
* webサーバの接続確認
* ネットワーク管理の基本コマンド


### グループ

★リーダが欠席の場合：（１）先頭から循環順序で決定（２）２回以上している場合は次の人に

* がついている人が、班の中の今日のリーダです
* 毎回の授業で、リーダの人が代表して sudo コマンドを実行します
* リーダー以外の人がsudo コマンドを実行してはいけません。

```
1班

1611140053
1811140016
1811140051
1811140031
1811140025
L 1811140077

２班

1811140075
1811140063
1611140017
1811140045
1811140057
L 1811140020

３班

1811140007
1811140058
1611140076
1811140036
1811140010
L 1811140024

４班

1811140054
1811140070
1811140040
1811140053
1811140038
L 1811140068

５班

1611140051
1811140080
2011141001
1811140033
1811140030
L 1811140067

６班

1711140059
1811140052
1811140032
1811140079
1811140023
L 1811140008

７班

1711140016
1811140012
1811140061
1811140022
1811140002
L 1811140078

８班

1811140042
1811140044
1811140015
1811140017a
1811140066
L 1811140001

９班

1711140049
1811140029
1811140019
1811140011
1811140037
L 1811140050

10班

1811140064
1811140071
1811140034
1811140003
1811140073
L 1811140014
```


## 担当ルータ


| R    | A0   | A1   | A2   | B0   | B1   | B2   | C0   | C1   | C2   |
| :--- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 9班  |10班 | 1班  | 2班  | 3班  | 4班  | 5班  | 6班  | 7班  | 8班 |



## ネットワーク構成２

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

## 各班のリーダを決める

## sshサーバにログイン

power shell などで ssh コマンド

```
ssh ユーザID@106.157.214.199
```

## 各班の担当ルータのルーティングテーブルを作成する

* 今回の課題に記載する
* 自分の担当ルータのインターーフェース名やIPアドレスを確認する



### quagga ripd のインストール(ダメ押し）

```bash
sudo apt install -y quagga
sudo apt install -y quagga-doc

sudo cp /usr/share/doc/quagga-core/examples/zebra.conf.sample /etc/quagga/zebra.conf
sudo cp /usr/share/doc/quagga-core/examples/ripd.conf.sample /etc/quagga/ripd.conf
```

## quagga でRIPの設定

* ルーティングテーブルが完成していないので直接はsshで入れない
* 自分の担当のルータに移動する（ルータを一つずつ移動する）

## 自分の班のルータのネットワークアドレスとインターフェース名を確認

自分のルータのIPアドレス

```bash
ip addr
```

Rの場合

```
wlp0s20f3: ...  inet 192.168.0.27/27
eno1: ...  inet 192.168.0.36/27
```

* ネットワークアドレスはネットワーク構成図でチェックする

R の場合、192.168.0.0/27

## quaggaのRIPの設定ファイルを修正

リーダーが代表して実施

```bash
cd /etc/quagga
ls
sudo nano ripd.conf
```

修正前

```
! -*- rip -*-
!
! RIPd sample configuration file
!
! $Id: ripd.conf.sample,v 1.1 2002/12/13 20:15:30 paul Exp $
!
hostname ripd
password zebra
!
! debug rip events
! debug rip packet
!
router rip
! network 11.0.0.0/8
! network eth0
! route 10.0.0.0/8
! distribute-list private-only in eth0
!
!access-list private-only permit 10.0.0.0/8
!access-list private-only deny any
!
!log file ripd.log
!
log stdout


```

修正後

* 直接接続しているネットワークアドレスとインターフェース名を設定する

```
! -*- rip -*-
!
! RIPd sample configuration file
!
! $Id: ripd.conf.sample,v 1.1 2002/12/13 20:15:30 paul Exp $
!
hostname ripd
password zebra
!
! debug rip events
! debug rip packet
!
router rip
 network （直接接続しているネットワークアドレス/サブネット１）
 network （直接接続しているネットワークアドレス/サブネット２）
 network インターフェース名１
 network インターフェース名２
! route 10.0.0.0/8
! distribute-list private-only in eth0
!
!access-list private-only permit 10.0.0.0/8
!access-list private-only deny any
!
!log file ripd.log
!
log stdout

```

Rの例

```
! -*- rip -*-
!
! RIPd sample configuration file
!
! $Id: ripd.conf.sample,v 1.1 2002/12/13 20:15:30 paul Exp $
!
hostname ripd
password zebra
!
! debug rip events
! debug rip packet
!
router rip
 network 192.168.0.0/27
 network 192.168.0.32/27
 network wlp0s20f3
 network eno1
! route 10.0.0.0/8
! distribute-list private-only in eth0
!
!access-list private-only permit 10.0.0.0/8
!access-list private-only deny any
!
!log file ripd.log
!
log stdout

```

## ripd の再起動

```bash
sudo service zebra restart
sudo service ripd restart
```

## tcpdump でRIPパケットを監視する

★（sudo コマンドですが全員実行していいです）

RIP はUDPでポート番号520

```bash
sudo tcpdump port 520 -v
```

## ルーティングテーブルの変化を確認する

* 30秒ごとに確認
* ★ 192.168.0.112/28 への経路の変化を確認

```bash
ip r
```

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



