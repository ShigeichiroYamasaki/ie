# インターネット工学演習 04

## ルータの基本

### host名の設定

```
sudo hostnamectl set-hostname <ホスト名>
```

### ipfoward の設定

```
 sudo nano /etc/sysctl.conf
```


2行コメントをはずす


```
# Uncomment the next line to enable packet forwarding for IPv4
net.ipv4.ip_forward=1

# Uncomment the next line to enable packet forwarding for IPv6
#  Enabling this option disables Stateless Address Autoconfiguration
#  based on Router Advertisements for this host
net.ipv6.conf.all.forwarding=1

```

再起動

```
sudo reboot
```

### ip route コマンドの確認

```bash
ip route
```

登録

```
sudo ip r add 宛先ネットワーク/サブネット via ゲートウェアドレス  dev ネットワークインタフェス
```

### traceroute コマンド

すべてのノードの経路を調べる

```bash
traceroute IPアドレス
```

### netplanコマンドの設定ファイル

/etc/netplan/99_config.yaml

```
sudo nano /etc/netplan/99_config.yaml
```

```
network:
  version: 2
  renderer: networkd
  ethernets:
    eth0:
      dhcp4: false
      dhcp6: false
      addresses: [192.168.1.4/28]
      gateway4: 192.168.1.1
      nameservers:
        addresses: [8.8.8.8, 8.8.4.4]
      routes:
      - to: 192.168.1.32/28
        via: 192.168.1.2
    eth1:
      dhcp4: false
      dhcp6: false
      addresses: [192.168.1.17/24]
      nameservers:
        addresses: [8.8.8.8, 8.8.4.4]
      routes:
      - to: 192.168.1.32/28
        via: 192.168.1.18
      - to: 192.168.1.48/28
        via: 192.168.1.18
```




# -------------------------------------
## ルータの配布

* 班の3人ごとに1台のルータを配布
* ルータに電源の入力
* リセットボタンをボールペンの先で20秒程度押して設定をリセットする

## ルータの接続
### 事前の状態

* 机のハブから6台のlinux PC にLANケーブルで接続されている
* 机のハブとサーバルームからのLANケーブルが接続されている

### 変更

1. 机のハブから6台のlinux PC にLANケーブルをはずす
2. 1台のルータのLAN側ポートと3台のLinux PC をLANケーブルで接続する
3. 班ごとに机のハブから2台のルータのWANポートにLANケーブルで接続する

## linuxマシンの設定確認

* ネットワーク接続設定がDHCPでの自動接続であることを確認する
* インターネットに接続できていることを確認する


## ルータの基本設定

1. ブラウザからルータにアクセスする (192.168.11.1)
2. ユーザ名：root パスワードなしでログインする
3. 機能を確認する

### LAN設定の修正

LAN側のIPアドレスを変更してみる

### ping で確認




