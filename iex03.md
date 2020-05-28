# インターネット工学演習 03
## インターネットの原理

## ロケール（言語）の変更

```
export LANG="en_US"

echo $LANG

```


## パスワードの変更

passwd コマンド

```
passwd

Old Password:

新しいパスワードを２回入れる
```



## IPアドレス関係情報の確認

```
$ ip addr

$ ifconfig
```

### 自分のIPアドレス関係情報の確認する

* Windows Powershell の場合

```
ipconfig
```

* Mac ターミナルの場合

```
ifconfig
```

* インターフェース名（有線、無線LAN、ローカルループバック）
* ipアドレス
* サブネットマスク
* ブロードキャストアドレス
* MACアドレス (ether)

## ルーティングテーブルの確認

```
$ ip r

default via 192.168.0.1 dev wlp0s20f3 proto static metric 600 
169.254.0.0/16 dev wlp0s20f3 scope link metric 1000 
192.168.0.0/27 dev wlp0s20f3 proto kernel scope link src 192.168.0.27 metric 600 
192.168.0.32/27 dev eno1 proto kernel scope link src 192.168.0.36 metric 100 
192.168.0.64/27 via 192.168.0.35 dev eno1 
192.168.0.96/27 via 192.168.0.35 dev eno1 
192.168.0.128/27 via 192.168.0.34 dev eno1 
192.168.0.160/27 via 192.168.0.34 dev eno1 
192.168.0.192/27 via 192.168.0.33 dev eno1 
192.168.0.224/27 via 192.168.0.33 dev eno1 

```

* デフォルトゲートウェイの確認
* 

## ARPテーブルの確認

```
$ arp
```

* MACアドレスとIPアドレスの対応

## ping による導通確認

確認したい相手のIPアドレスを知る

```
R $ ping 192.168.0.35

PING 192.168.0.35 (192.168.0.35) 56(84) bytes of data.
64 bytes from 192.168.0.35: icmp_seq=1 ttl=64 time=0.326 ms
64 bytes from 192.168.0.35: icmp_seq=2 ttl=64 time=0.530 ms
64 bytes from 192.168.0.35: icmp_seq=3 ttl=64 time=0.715 ms
64 bytes from 192.168.0.35: icmp_seq=4 ttl=64 time=0.681 ms
64 bytes from 192.168.0.35: icmp_seq=5 ttl=64 time=0.688 ms
64 bytes from 192.168.0.35: icmp_seq=6 ttl=64 time=0.244 ms
64 bytes from 192.168.0.35: icmp_seq=7 ttl=64 time=0.690 ms
64 bytes from 192.168.0.35: icmp_seq=8 ttl=64 time=0.742 ms


(コントロール ｃ) で終了する
```

* そのマシンまでの往復時間を確認する

### 様々なサイトにping してみる

* GOOGLEのDNSサーバ  8.8.8.8
* yahoo のサーバ www.yahoo.co.jp
* 近畿大学産業理工学部のDNSサーバ 157.13.1.1

### ping した後にARPテーブルを再確認する

```
$ arp
```

## traceroute で経路を確認する

```
$ traceroute 8.8.8.8

traceroute to 8.8.8.8 (8.8.8.8), 64 hops max, 52 byte packets
 1  ia201wl4 (192.168.0.1)  7.978 ms  5.241 ms  5.784 ms
 2  oha-mx480-bbbas05.qtnet.ad.jp (218.40.227.156)  10.688 ms  10.055 ms  9.346 ms
 3  211.132.104.33 (211.132.104.33)  9.649 ms
    211.132.104.37 (211.132.104.37)  11.368 ms
    211.132.104.33 (211.132.104.33)  9.512 ms
 4  61.203.192.241 (61.203.192.241)  11.010 ms
    61.203.192.237 (61.203.192.237)  11.930 ms
    61.203.192.249 (61.203.192.249)  10.036 ms
 5  61.203.193.126 (61.203.193.126)  25.828 ms
    61.203.193.122 (61.203.193.122)  24.705 ms  25.398 ms
 6  61.203.192.177 (61.203.192.177)  23.924 ms  27.273 ms  24.774 ms
 7  108.170.242.129 (108.170.242.129)  26.158 ms  26.731 ms
    108.170.242.161 (108.170.242.161)  24.342 ms
 8  64.233.174.187 (64.233.174.187)  26.882 ms
    72.14.236.107 (72.14.236.107)  23.827 ms
    209.85.250.45 (209.85.250.45)  23.553 ms
 9  google-public-dns-a.google.com (8.8.8.8)  26.772 ms  24.187 ms  24.120 ms

```

いろいろなサイトまでの経路を確認する

* 演習ネットワークの全マシンのIPアドレス
* yahoo のサーバ www.yahoo.co.jp
* 近畿大学産業理工学部のDNSサーバ 157.13.61.1
* 九工大のwebサーバ  www.kyutech.ac.jp

## whois データベースの確認

### 近畿大学産業理工学部のIPアドレスのwhoisデータベース情報の確認

```
$ whois 157.13.1.1
```

いろいろなIPアドレスの whois データベースの情報を確認する

* 8.8.8.8
* 1.1.1.1
* traceroute の途中経路のIPアドレスの情報を確認する

## DNS関連情報

```
$ dig
```

### host コマンドでIPアドレスを確認する

```
$ host www.kindai.ac.jp
```
### host コマンドでnsレコードを確認する

```
$ host -t ns kindai.ac.jp
```

## IPアドレスを手動設定する

* IPアドレスとサブネットマスクの確認
* DNSサーバのIPアドレスの確認
* デフォルトゲートウェーの確認

