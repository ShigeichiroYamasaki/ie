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
ping6 2001:4860:4860::6464

ping6 2001:4860:4860::8888
```

#### google のipv6アドレスの確認

```
host -t AAAA ipv6.google.com
 
 
2404:6800:4004:80b::200e
```

```
ping6 2404:6800:4004:80b::200e

ping6 ipv6.google.com
```

## ping による速度測定

### ipv4の速度

google.com


```
ping -c 10 -s 14000 -i 0.5 google.com
```

### ipv6の速度


```
ping6 -c 10 -s 1400 -i 0.5 google.com
```

## traceroute

```
traceroute6 ipv6.google.com
```

## 近隣探索(Neighbor Discovery for IP version 6)

ARP にあたるip アドレスとMACアドレスの対応を知る方法

```
ip -6 neigh
```
