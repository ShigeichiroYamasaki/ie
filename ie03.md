# インターネット工学演習 03

## LANインターフェスの設定


### ファイルの内容を見るコマンド

	cat       ファイルの中を全部表示する

	less　　	ファイルの中を少しずつ表示する

 例
 
```
$ cat /etc/bashrc 
```
    
### 隣の人のIPアドレスを確認する
    
それぞれ以下のコマンドを実行してIPアドレスを隣の人に教える

	 ip addr		ネットワーク・インターフェースごとのipアドレスなどの情報を表示させる


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
    
### ●カレントディレクトリの確認
    
```
$ pwd
```

## 利用者の登録

```
$ sudo adduser <ユーザ名>
```

   パスワードを２回入れる
   （パスワードはエコーバックされない）

## nanoエディタの使い方

```
$ nano <ファイル名>
```

### 画面の下のメニューの見方

  ^X などは、controlキーを押しながらｘを押すという意味
   M-X などは、escキーを押してxを押すという意味

### 編集したデータの保存方法

    ^X して　Y で保存終了

### カットアンドペースト

    ^K でカットして、^U で貼り付け

### 文字列の検索

    ^W 検索文字列

## 環境変数の確認

```
$ printenv
```

```
$ printenv PATH
```

## 環境変数の変更

```
$ export export PS1="> "
$ export export PS1="$ "
```
    
## ネットワークインターフェースの確認

```
$ ifconfig
    
$ ip addr
    
$ sudo arp -a
    
$ ping <隣の人のIPアドレス>
```

## シャットダウンの方法

```
$ shutdown -h now
```

## シェルの環境設定


```
$ cd ~
$ ls -a
```
    
### ~/.bashrc の編集

```    
$ nano .bashrc
```    
    
    

