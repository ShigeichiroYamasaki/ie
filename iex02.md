# インターネット工学演習 02
## Linuxの設定と基本操作

### sshでサーバに接続して以下の操作を行う

* ubuntu のターミナルでssh 接続
* windows のpower shell でssh 接続
* Mac のターミナルで ssh 接続

#### 以下，結果をメモしていく

## 現在のディレクトリのパスの確認

```
$ pwd
```


## ディレクトリへの移動


```
$ cd ~
$ pwd

$ cd /
$ pwd

$ cd /usr/local
$ pwd

```

## 現在のディレクトリのファイルの一覧

```
$ ls

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

## IPアドレスの確認

自分のIPアドレスを確認してください

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

`    ^X などは、controlキーを押しながらｘを押すという意味`
`    M-X などは、escキーを押してxを押すという意味`

#### 編集したデータの保存方法

` ^O ファイル名を確認して enter で保存`

  
#### カットアンドペースト
 
`   ^K でカットして、^U で貼り付け`
 
#### 文字列の検索

`    ^W 検索文字列`

#### 終了

`     ^X 終了`

### ssh でリモートログイン

```
ssh kindai@192.168.1.X
```


### 演習ネットワーク

```
                         Internet
                              |
              253             1         
    -----------+--------------+------------------------------------------------------ 192.168.0.0/24
        [ router1 ](SSHサーバ)   
               |                   
               |
  2    3   4   1  18  19  34  35  50  66  67  82  83  98  99 114 130 131 146 147 162
--+----+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+- 192.168.1.0/24
 G8R  G4R G1R     G2R G1  G3R G2  G3  G5R G4  G6R G5  G7R G6  G7  G9R G8 G10R G9 G10
 
```
