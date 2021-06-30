# インターネット工学演習 15

# IPv6

## ip アドレスの確認

```
ip -6 a
```

* グローバルユニキャストアドレスの確認
* eno1 の 240f:で始まるアドレスをメモ

* リンクローカルユニキャストアドレスの確認
* eno1 の fe80:: で始まるアドレスをメモ


### ipv6 ルーティングテーブルの確認

```
ip -6 r
```

#### DNS でIPv6アドレスを確認

## DNSの　ipv6 アドレス

google public DNS v6

```
host dns64.dns.google

dns64.dns.google has IPv6 address 2001:4860:4860::64
dns64.dns.google has IPv6 address 2001:4860:4860::6464
```


#### ping6　で ipv6 のDNSサーバまでping をかけてみる

```
ping6 2001:4860:4860::64
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
traceroute google.com
```

### DNS でIPアドレスを確認

```
host -t AAAA google.com
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

## ping による速度測定

### ipv4の速度

google.com

```
host -t A google.com
```


```
ping -c 5 -s 1400 -i 0.5 172.217.161.206
```

### ipv6の速度

```
host -t AAAA google.com
```


```
ping6 -c 5 -s 1400 -i 0.5 2404:6800:400a:80b::200e
```


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

 