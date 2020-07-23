# インターネット工学演習 15
## IPv6

## ipv6アドレスの確認

```
ip a
```

```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eno1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 1c:69:7a:04:ea:9f brd ff:ff:ff:ff:ff:ff
    inet 192.168.0.29/27 brd 192.168.0.31 scope global noprefixroute eno1
       valid_lft forever preferred_lft forever
    inet6 240f:ca:425:1:65d2:b6ef:e501:6e79/64 scope global temporary dynamic 
       valid_lft 289sec preferred_lft 289sec
    inet6 240f:ca:425:1:40d2:5e8e:9f09:82ab/64 scope global temporary deprecated dynamic 
       valid_lft 289sec preferred_lft 0sec
    inet6 240f:ca:425:1:2d7d:3f2b:4188:6688/64 scope global temporary deprecated dynamic 
       valid_lft 289sec preferred_lft 0sec
    inet6 240f:ca:425:1:1c8e:6cf3:87da:1b0b/64 scope global temporary deprecated dynamic 
       valid_lft 289sec preferred_lft 0sec
    inet6 240f:ca:425:1:6807:8227:1fdd:4a9f/64 scope global temporary deprecated dynamic 
       valid_lft 289sec preferred_lft 0sec
    inet6 240f:ca:425:1:409d:3b67:5927:5e62/64 scope global temporary deprecated dynamic 
       valid_lft 289sec preferred_lft 0sec
    inet6 240f:ca:425:1:6126:d02d:257f:45e2/64 scope global temporary deprecated dynamic 
       valid_lft 289sec preferred_lft 0sec
    inet6 240f:ca:425:1::4/128 scope global dynamic noprefixroute 
       valid_lft 3571sec preferred_lft 1771sec
    inet6 240f:ca:425:1:db2a:a383:b66d:ccc9/64 scope global dynamic mngtmpaddr noprefixroute 
       valid_lft 289sec preferred_lft 289sec
    inet6 fe80::96ec:bc43:b8b:d8e3/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
3: wlp0s20f3: <BROADCAST,MULTICAST> mtu 1500 qdisc noqueue state DOWN group default qlen 1000
    link/ether 98:2c:bc:e9:0b:5b brd ff:ff:ff:ff:ff:ff

```

### グローバルユニキャストアドレスの確認


 inet6 240f:ca:425:1:65d2:b6ef:e501:6e79/64 scope global temporary dynamic 
 
### DNS でIPv6アドレスを確認


 
 
### ping6
 
 ```
 ping6 240f:ca:425:1:65d2:b6ef:e501:6e79
 ```
 
### netstat
 
 ```
 netstat -rnA inet6
 ```

### AS``

```
curl http://api.db-ip.com/v2/free/240f:ca:425:1:985f:f0eb:24c8:aa1e
``` 
 