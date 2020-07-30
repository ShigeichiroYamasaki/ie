# インターネット工学演習 15
# IPv6

# 間違ってSSHサーバのアカウントを消してしまいました！

* 共通のIDとパスワードでログインしてもらいます。

* ログイン後は，これまでと同じです。

### サーバの鍵を消さないと接続できません。


## Windows 10  PowerShell の場合

.ssh というファイルがサーバの鍵です

```
cd ~
rm .ssh
```
 
## Windows 10 Putty の場合

すみません。難しいので PowerShell でやってください

## MacOSX ターミナルの場合

```
cd ~
rm -fr .ssh
```

# SSHログイン(IPアドレス 106.157.214.199)

### kindai という共通ユーザIDでログインしてください

* ID: kindai
* パスワード：nas......jin

```bash
ssh kindai@106.157.214.199
```

### Rマシンへssh (これまで同様自分のアカウントでログインできます）

```bash
ssh ユーザID@192.168.0.27
```

#### ipv6アドレスの確認

```
ifconfig
```

```
ip -6 a
```

#### netstat
 
 ```
 netstat -rnA inet6
 ```

#### グローバルユニキャストアドレスの確認

* eno1 の 240f:で始まるアドレスをメモ


### リンクローカルユニキャストアドレスの確認

* eno1 の fe80:: で始まるアドレスをメモ


#### グローバルユニキャストアドレスの確認


## デフォルト　ルータの ipv6アドレス

```
IPv6アドレス/プレフィックス長
(グローバルユニキャストアドレスの確認)	240f:ca:425:1:fab7:97ff:fe49:b4fa/64

IPv6アドレス/プレフィックス長
(リンクローカルアドレス)	fe80::fab7:97ff:fe49:b4fa/64
```

#### DNS でIPv6アドレスを確認

## DNSの　ipv6 アドレス

山崎家のプロバイダのDNS

```
2001:268:fd07:4::1
```

```
whois 2001:268:fd07:4::1
```


#### ping6　で ipv6 のDNSサーバまでping をかけてみる

```
ping6 2001:268:fd07:4::1
```

#### google のipv6アドレスの確認

```
host -t AAAA ipv6.google.com
 
 
2404:6800:4004:80b::200e
 
ping6 2404:6800:4004:80b::200e
```

```
ping6 ipv6.google.com
```

## traceroute

```
traceroute ipv6.google.com
```

### DNS でIPアドレスを確認

```
host -t AAAA google.com
```

### C0マシンへssh (これまで同様自分のアカウントでログインできます）

```bash
ssh ユーザID@192.168.0.33
```


#### ipv6アドレスの確認

```
ifconfig
```

```
ip -6 a
```


#### netstat
 
 ```
 netstat -rnA inet6
 ```


### B0マシンへssh 

```bash
ssh ユーザID@192.168.0.34
```


#### ipv6アドレスの確認

```
ifconfig
```

```
ip -6 a
```


#### netstat
 
 ```
 netstat -rnA inet6
 ```
 
#### グローバルユニキャストアドレスの確認

#### DNS でIPv6アドレスを確認



### A0マシンへssh (これまで同様自分のアカウントでログインできます）

```bash
ssh ユーザID@192.168.0.35
```


#### ipv6アドレスの確認

```
ifconfig

```

### netstat
 
 ```
 netstat -rnA inet6
 ```
 
## ipv6ではルーティングできていない

以下は失敗する

```
ping6 2404:6800:4004:818::200e
```

 