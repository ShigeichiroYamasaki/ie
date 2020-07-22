# インターネット工学演習 12
## ネットワーク性能測定

## web技術の続き

```ssh
ssh ユーザID＠106.157.214.199
```

### スクリプトエイリアス用ディレクトリへ移動

```bash
cd /usr/lib/cgi-bin/

sudo mkdir（自分の学籍番号または名前)

sudo chown ユーザID:ユーザID （自分の学籍番号または名前)

cd （自分の学籍番号または名前)
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


## 担当ルータ(マシン）


| R    | A0   | A1   | A2   | B0   | B1   | B2   | C0   | C1   | C2   |
| :--- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 9班  |10班 | 1班  | 2班  | 3班  | 4班  | 5班  | 6班  | 7班  | 8班 |

## ポートマッピング

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


## apache2 のポートの変更

```bash
sudo nano /etc/apache2/ports.conf
```

以下の例（8001）のように 80 以外のポート番号に変更する

```
Listen: 8001 
```

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



## ネットワーク性能評価ツールのインストール

### 事前にOS をupdate, upgradeしておく

```bash
sudo apt update
sudo apt -y upgrade
```

### apache bench

apacheをインストールすると自動的にインストールされる

### ping

不要

### iperf3

```bash
sudo apt install -y iperf3
```

### munin

```bash
sudo apt install -y libcgi-fast-perl libapache2-mod-fcgid
sudo apt install -y munin munin-node munin-plugins-extra
```

```bash
sudo systemctl start munin-node
sudo systemctl restart apache2
```

### munin.conf

```
sudo nano /etc/munin/munin.conf
```

以下のように修正

```
# Example configuration file for Munin, generated by 'make build'

# The next three variables specifies where the location of the RRD
# databases, the HTML output, logs and the lock/pid files. They all
# must be writable by the user running munin-cron. They are all
# defaulted to the values you see here.
#
dbdir /var/lib/munin
htmldir /var/cache/munin/www
logdir /var/log/munin
rundir /var/run/munin

# Where to look for the HTML templates
#
tmpldir /etc/munin/templates

# Where to look for the static www files
#
#staticdir /etc/munin/static

# temporary cgi files are here. note that it has to be writable by
# the cgi user (usually nobody or httpd).
#
# cgitmpdir /var/lib/munin/cgi-tmp

# (Exactly one) directory to include all files from.
includedir /etc/munin/munin-conf.d
[...]
# a simple host tree
[server1.example.com]
 address 127.0.0.1
 use_node_name yes
[...]
```

### apache24.conf

```
sudo mv /etc/munin/apache24.conf /etc/munin/apache24.conf_bak
```

```
sudo nano /etc/munin/apache24.conf
```

以下をペースト

```
Alias /munin /var/cache/munin/www
<Directory /var/cache/munin/www>
 # Require local
 Require all granted
 Options FollowSymLinks SymLinksIfOwnerMatch
 Options None
</Directory>

ScriptAlias /munin-cgi/munin-cgi-graph /usr/lib/munin/cgi/munin-cgi-graph
<Location /munin-cgi/munin-cgi-graph>
 # Require local
 Require all granted
 Options FollowSymLinks SymLinksIfOwnerMatch
 <IfModule mod_fcgid.c>
 SetHandler fcgid-script
 </IfModule>
 <IfModule !mod_fcgid.c>
 SetHandler cgi-script
 </IfModule>
</Location>
```

### Restart Apache:

```
sudo service apache2 restart
sudo service munin-node restart
```



## apache bench

WEBサーバの性能測定

WEBサーバのパフォーマンスデバッギング

* Apache Benchは、DOS攻撃にも使えるツールです!! 使用する際は十分注意してください!!

* Apacheで標準に付いているWEBサーバの性能を計測するためのコマンド


|オプション名	|説明|
|:--:|:--:|
|-n 数値	|リクエストの総数を数値で指定|
|-c 数値	|同時に発行するリクエストの数を数値で指定|
|-t 数値	|サーバからのレスポンスの待ち時間（秒）を数値で指定|
|-A ユーザー名:パスワード	|ベーシック認証が必要なコンテンツにテストする|
|-P ユーザー名:パスワード	|認証の必要なプロキシを通じてテストする|
|-X プロキシサーバ名:ポート番号	|プロキシ経由でリクエストする場合に指定|
|-V	|バージョンを表示|
|-h	|ヘルプを表示|

#### 使用法

隣の人のマシンのIPアドレスを調べる


```bash
ab -n 10000 -c 100 http://隣の人のIPアドレス
ab -n 10000 -c 100 http://192.168.0.27/
```

* Complete requestsが正常に処理したリクエスト数
* Failed requestsは、処理に失敗したリクエスト数

* 何リクエストまで耐えられるか
	* Failed requests: を見る
	
	
	-n と -cの値を増やしていく


* 秒間どれくらいのリクエストをさばけるか？
	* Requests per second　を見る

* パフォーマンス
	* Time per request: を見る

## ping による速度測定

* pingコマンドの主なオプション

|オプション 引数	|意味|
|:--|:--|
|-c 数	|パケットの送信回数を指定する|
|-i 秒	|パケットの送信間隔を秒単位で指定する|
|-n	|数値のみ出力する（名前解決を行わない）|
|-r	|ホストへ直接パケットを送信する（ルーティングしない）|
|-R	|パケットの経路を表示する|
|-q	|コマンド実行開始時と終了時のメッセージのみを表示します。|
|-s サイズ	|パケットサイズをバイト単位で指定する（初期値は56）|
|-t TTL値	|パケットのTTL（Time to Live）値を指定する|
|-v	|詳細情報を表示する|

```bash
ping -c 5 -s 1400 -i 0.5 157.13.1.1
```

パケットサイズはフラグメントを起こさないサイズでないとTTLが測定できない


## iperf3 

* サーバとクライアントで測定する
* グループ内で互いのIPアドレスを確認する

#### サーバ側

```bash
iperf3 -s
```

#### クライアント側

```bash
iperf3 -c 
```

[https://sourceforge.net/speedtest/](https://sourceforge.net/speedtest/)

## munin

自分のmunin サイトを確認

* 1時間程度経過した後

```
http://106.157.214.199:8010/munin
```

