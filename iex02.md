# インターネット工学演習 02

## 現在のディレクトリのパスの確認

```
$ pwd
/home/yamasaki

```

## ディレクトリへの移動

```
$ cd ~
$ pwd
/home/yamasaki
$ cd /
$ pwd
/
$ cd /usr/local
$ pwd
/usr/local

```

## 現在のディレクトリのファイルの一覧

```
$ ls
ビデオ   ダウンロード テンプレート  デスクトップ  公開
ピクチャ  ミュージック ドキュメント
```

###  ls コマンドに -l オプションをつけると詳細情報が表示される

```
$ ls -l
total 36
drwxr-xr-x 2 yamasaki yamasaki 4096 Jul 19  2018 ビデオ
drwxr-xr-x 2 yamasaki yamasaki 4096 Jul 19  2018 ピクチャ
drwxr-xr-x 2 yamasaki yamasaki 4096 Jul 19  2018 ダウンロード
drwxr-xr-x 2 yamasaki yamasaki 4096 Jul 19  2018 ミュージック
drwxr-xr-x 2 yamasaki yamasaki 4096 Jul 19  2018 テンプレート
drwxr-xr-x 2 yamasaki yamasaki 4096 Jul 19  2018 ドキュメント
drwxr-xr-x 3 yamasaki yamasaki 4096 Feb 17 10:47 デスクトップ
drwxr-xr-x 7 yamasaki yamasaki 4096 Apr 17 08:30 公開

```

## ネットワークの現在の設定の確認

```
$ ifconfig

enp3s0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.0.18  netmask 255.255.255.0  broadcast 192.168.0.255
        inet6 fe80::8aa6:d0ba:d83d:c568  prefixlen 64  scopeid 0x20<link>
        ether 74:d4:35:c6:0b:b3  txqueuelen 1000  (Ethernet)
        RX packets 58152998  bytes 26208402394 (26.2 GB)
        RX errors 0  dropped 3153977  overruns 0  frame 0
        TX packets 40433145  bytes 5928281714 (5.9 GB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 1474075  bytes 144875568 (144.8 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 1474075  bytes 144875568 (144.8 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

```

## IPアドレスの確認

```
$ ip addr

1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: enp3s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 74:d4:35:c6:0b:b3 brd ff:ff:ff:ff:ff:ff
    inet 192.168.0.18/24 brd 192.168.0.255 scope global noprefixroute enp3s0
       valid_lft forever preferred_lft forever
    inet6 fe80::8aa6:d0ba:d83d:c568/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
3: wlp2s0: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN group default qlen 1000
    link/ether 54:27:1e:9e:9f:27 brd ff:ff:ff:ff:ff:ff

```


## 新しいディレクトリの作成

```
$ mkdir kadai
$ ls
ビデオ	  ダウンロード	テンプレート  デスクトップ  kadai
ピクチャ  ミュージック	ドキュメント  公開

```

## 新しいファイルの作成

```
$ touch test
$ ls
test

```

## ファイルのコピー

```
$ cp test test1
$ ls
test  test1

```

## ファイルの移動

```
$ mkdir work
$ ls
test  test1  work
$ mv test work
$ ls
test1  work
$ cd work/
$ ls
test

```

## ファイル名の変更

```
$ mv test test100
$ ls
test100

```

## ファイルの削除

```
$ ls
test100
$ rm test100 
$ ls

```

## 標準デバイス名の確認方法

### ネットワークカード


```
$ ip addr
1: lo: <LOOPBACK,UP,LOWER_UP>
...
2: enp3s0: <BROADCAST,MULTICAST,UP,LOWER_UP>
...
3: wlp2s0: <BROADCAST,MULTICAST> 

```

### ハードディスク（SSD)

```
$ df
Filesystem ...
/dev/disk1s1   ...
...
/dev/disk2s1   ...

```

## cd コマンドでホームディレクトに移動

```
$ cd ~
$ pwd
/home/kindai

```


## sudo コマンド

```
$ cd /
$ touch gomi
touch: gomi: Permission denied
$ sudo touch gomi
Password:
$ sudo rm gomi
```

## 環境変数を確認する

### echo コマンド

```
$ echo $LANG
ja_JP.UTF-8
$ echo $SHELL
/bin/bash
$ echo $USER
kindai

```

## 環境変数を設定する

```
$ echo $LANG
ja_JP.UTF-8
$ echo $SHELL
/bin/bash
$ echo $USER
kindai

```


## 環境変数 LANG変更の例

```
$ export LANG=ja_JP.UTF-8
$ date +%x
2019年04月17日
$ export LANG=en_GB.UTF-8
$ date +%x
17/04/19
$ export LANG=en_US.UTF-8
$ date +%x
04/17/2019

```

## 環境変数 PATH

```
$ echo $PATH

```


## nanoエディタの使い方

### 画面の下のメニューの見方

*    ^X などは、controlキーを押しながらｘを押すという意味
*    M-X などは、escキーを押してxを押すという意味

#### 編集したデータの保存方法

*     ^X して　Y で保存終了
  
#### カットアンドペースト
 
 *   ^K でカットして、^U で貼り付け
 
#### 文字列の検索

*    ^W 検索文字列

## ssh のインストール

```
sudo apt install ssh
```

### 各マシンでのIPアドレスの確認

```
ip addr
```

IP アドレスを確認し、隣同士でIPアドレスを教える

	i92.268.1.X
	
### ssh でリモートログイン

```
ssh kindai@192.168.1.X
```

# 提出レポートURL

第２回レポート
[https://forms.gle/dTk3SZ38G9Y6eZdq9](https://forms.gle/dTk3SZ38G9Y6eZdq9)

