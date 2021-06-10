# インターネット工学演習 09

## tcpdump でRIPパケットを監視する

22番ポート(ssh)を盗聴

```bash
sudo tcpdump port 22 -Xa
```


### 11セグメント（16セグメント）の例（第４段階）

★サブネットマスクが27ビットと28ビットになっていることに注意！

```
                                     Internet
                                         |
                        253              1           
    ----------------------+--------------+----------- 192.168.0.0/24
                      [ router1 ](SSH)
                          |
                          |
  2       3       4       1    18     
--+-------+-------+-------+----+--------------------- 192.168.1.0/28
[G8R]   [G4R]   [G1R]          
  |       |       |
  |       |       |
  |       |       17          18    19
  |       |      -+------------+-----+--------------- 192.168.1.16/28
  |       |                  [G2R]  G1 
  |       |                    |
  |       |                    |
  |       |                   33    34    35    
  |       |                 ---+-----+-----+--------- 192.168.1.32/28
  |       |                        [G3R]   G2      
  |       |                          |
  |       |                          |
  |       |                         49    50   
  |       |   -----------------------+-----+--------- 192.168.1.48/28
  |       |                               G3     
  |       |
  |       |
  |       65    66    67         
  |     --+-----+-----+------------------------------ 192.168.1.64/28
  |           [G5R]   G4    
  |             |
  |             |
  |            81          82    83
  |           --+-----------+-----+------------------ 192.168.1.80/28
  |                       [G6R]   G5  
  |                         |
  |                         |
  |                        97    98    99
  |                    -----+-----+-----+------------ 192.168.1.96/28
  |                             [G7R]  G6 
  |                               |
  |                               |
  |                              113   114  
  |                            ---+-----+------------ 192.168.1.112/28
  |                                    G7   
  |
  |
 129     130   131   
--+-------+-----+------------------------------------ 192.168.1.128/28
        [G9R]  G8     
          |
          |
         145   146   147
      ----+-----+-----+------------------------------ 192.168.1.144/28
             [G10R]   G9 
                |
                |
               161   162
            ----+-----+------------------------------ 192.168.1.160/28
                    G10
 


```


## 各班で，ルーティングテーブルを書いてください

* G1R
* G2R
* G3R
* G4R
* G5R
* G6R
* G7R
* G8R
* G9R
* G10R

```
ルータ名 router1
宛先ネットワーク／サブネット｜　ゲートウェイ　　｜　インターフェース
-------------------------------------------------------------------------------------
192.168.0.0/24      |直接|
192.168.1.0/28      |直接|
192.168.1.16/28     |192.168.1.4|
192.168.1.32/28     |192.168.1.4|
192.168.1.48/28     |192.168.1.4|
192.168.1.64/28     |192.168.1.3|
192.168.1.80/28     |192.168.1.3|
192.168.1.96/28     |192.168.1.3|
192.168.1.112/28    |192.168.1.3|
192.168.1.128/28    |192.168.1.2|
192.168.1.144/28    |192.168.1.2|
192.168.1.160/28    |192.168.1.2|
デフォルト            |192.168.0.1|
                		

```

### ルーティングテーブルを設定してください

ルータを１つずつたどって ssh ログインしていけばルータにたどり着けるように設定しています。


## 動的経路制御

RIPの実験


### quagga ripd のインストール（すべてのルータ）

```bash
sudo apt update
sudo apt upgrade -y


sudo apt install -y quagga
sudo apt install -y quagga-doc
```

### 設定ファイルのコピー


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

例

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
 network 192.168.1.0/28
 network 192.168.1.32/28
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

