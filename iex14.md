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

## SSHログイン(IPアドレス 106.157.214.199)

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

#### netstat
 
 ```
 netstat -rnA inet6
 ```

#### グローバルユニキャストアドレスの確認

* eno1 の 240f:で始まるアドレスをメモ


### リンクローカルユニキャストアドレスの確認

* eno1 の fe80:: で始まるアドレスをメモ
```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group 

### C0マシンへssh (これまで同様自分のアカウントでログインできます）

```bash
ssh ユーザID@192.168.0.33
```


#### ipv6アドレスの確認

```
ifconfig
```


#### netstat
 
 ```
 netstat -rnA inet6
 ```

#### グローバルユニキャストアドレスの確認

#### DNS でIPv6アドレスを確認

## DNSの　ipv6 アドレス

山崎家のプロバイダのDNS

```
2001:268:fd07:4::1
```

```
whois 2001:268:fd07:4::1
```

## ルータの ipv6アドレス

```
IPv6アドレス/プレフィックス長
(グローバル)	240f:ca:425:1:fab7:97ff:fe49:b4fa/64

IPv6アドレス/プレフィックス長
(リンクローカル)	fe80::fab7:97ff:fe49:b4fa/64
```

## ping6

```
ping6 240f:ca:425:1:fab7:97ff:fe49:b4fa
```

```
ping6 ipv6.google.com
```

## traceroute

```
traceroute ipv6.google.com
```

### B0マシンへssh (これまで同様自分のアカウントでログインできます）

```bash
ssh ユーザID@192.168.0.34
```


#### ipv6アドレスの確認

```
ifconfig
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

#### netstat
 
 ```
 netstat -rnA inet6
 ```

#### グローバルユニキャストアドレスの確認

#### DNS でIPv6アドレスを確認

```
 host google.com

google.com has address 172.217.161.206
google.com has IPv6 address 2404:6800:400a:80b::200e
google.com mail is handled by 20 alt1.aspmx.l.google.com.
google.com mail is handled by 10 aspmx.l.google.com.
google.com mail is handled by 30 alt2.aspmx.l.google.com.
google.com mail is handled by 40 alt3.aspmx.l.google.com.
google.com mail is handled by 50 alt4.aspmx.l.google.com.
```
 

### netstat
 
 ```
 netstat -rnA inet6
 ```
 
### DNS でIPアドレスを確認

```
host -t AAAA www.google.com
```

### ブラウザで確認

URL に　2404:6800:400a:808::2004　

### curlでwebページを取得

```
curl http://api.db-ip.com/v2/free/240f:ca:425:1:985f:f0eb:24c8:aa1e
``` 
 