# インターネット工学演習 09


## 動的ルーティングの実験

RIPの実験

### quagga ripd のインストール（すべてのルータ）

```bash
sudo apt install -y quagga
sudo apt install -y quagga-doc
```

### 設定ファイルの確認

```
cat /usr/share/doc/quagga-core/examples/zebra.conf.sample 
```

```
cat /usr/share/doc/quagga-core/examples/ripd.conf.sample
```


```
sudo cp /usr/share/doc/quagga-core/examples/zebra.conf.sample /etc/quagga/zebra.conf
sudo cp /usr/share/doc/quagga-core/examples/ripd.conf.sample /etc/quagga/ripd.conf
```

## quaggaのRIPの設定ファイルを修正

リーダーが代表して実施

```bash
cd /etc/quagga
ls
sudo nano ripd.conf
```

修正前

```
! -*- rip -*-
!
! RIPd sample configuration file
!
! $Id: ripd.conf.sample,v 1.1 2002/12/13 20:15:30 paul Exp $
!
hostname ripd
password zebra
!
! debug rip events
! debug rip packet
!
router rip
! network 11.0.0.0/8
! network eth0
! route 10.0.0.0/8
! distribute-list private-only in eth0
!
!access-list private-only permit 10.0.0.0/8
!access-list private-only deny any
!
!log file ripd.log
!
log stdout


```

修正後

* 直接接続しているネットワークアドレスとインターフェース名を設定する

```
! -*- rip -*-
!
! RIPd sample configuration file
!
! $Id: ripd.conf.sample,v 1.1 2002/12/13 20:15:30 paul Exp $
!
hostname ripd
password zebra
!
! debug rip events
! debug rip packet
!
router rip
 network （直接接続しているネットワークアドレス/サブネット１）
 network （直接接続しているネットワークアドレス/サブネット２）
 network インターフェース名１
 network インターフェース名２
! route 10.0.0.0/8
! distribute-list private-only in eth0
!
!access-list private-only permit 10.0.0.0/8
!access-list private-only deny any
!
!log file ripd.log
!
log stdout

```

Rの例

```
! -*- rip -*-
!
! RIPd sample configuration file
!
! $Id: ripd.conf.sample,v 1.1 2002/12/13 20:15:30 paul Exp $
!
hostname ripd
password zebra
!
! debug rip events
! debug rip packet
!
router rip
 network 192.168.0.0/27
 network 192.168.0.32/27
 network wlp0s20f3
 network eno1
! route 10.0.0.0/8
! distribute-list private-only in eth0
!
!access-list private-only permit 10.0.0.0/8
!access-list private-only deny any
!
!log file ripd.log
!
log stdout

```

## ripd の再起動

```bash
sudo service zebra restart
sudo service ripd restart
```

## tcpdump でRIPパケットを監視する

★（sudo コマンドですが全員実行していいです）

RIP はUDPでポート番号520

```bash
sudo tcpdump port 520 -v
```

## ルーティングテーブルの変化を確認する

* 30秒ごとに確認
* ★ 192.168.0.112/28 への経路の変化を確認

```bash
ip r
```

### ripd の起動

```bash
sudo service zebra start
sudo service ripd start
```


### ルーティングテーブルの確認


```bash
ip r
```

### ネットワークの切り離し

* ネットワークを物理的に切り離す
* ルーティングテーブルの自動的削除を確認する

```bash
ip r
```


### ネットワークの再接続

* 物理的に接続する
* ルーティングテーブルの自動的追加を確認

```bash
ip r
```

### ネットワークの接続変更

* 物理的に接続を変更
* IPアドレスなどの設定を変更
* ルーティングテーブルの自動的修正を確認

```bash
ip r
```

