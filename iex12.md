# インターネット工学演習 12
## WEBサーバの構築2

## レポートURL

[https://forms.gle/7XU3CJoTxsWQYEyK9
](https://forms.gle/7XU3CJoTxsWQYEyK9
)

## インストール

### 事前にOS をupdate, upgradeしておく

```bash
sudo apt update
sudo apt upgrade
```

### apache bench

apacheをインストールすると自動的にインストールされる

### ping

不要

### iperf3

```bash
sudo apt install iperf3
```

### munin

```bash
sudo apt install munin munin-node
```

```bash
sudo systemctl start munin-node
sudo systemctl restart apache2
```

 
## apache bench

WEBサーバの性能測定

WEBサーバのパフォーマンスデバッギング

* Apache Benchは、DOS攻撃にも使えるツールです!! 使用する際は十分注意してください!!

* Apacheで標準に付いているWEBサーバの性能を計測するためのコマンド


|オプション名	|説明|
|:--:|:--:|
|-n 数値	|リクエストの総数を数値で指定|
|-c 数値	|同時に発行するリクエストの数を数値で指定|
|-t 数値	|サーバからのレスポンスの待ち時間（秒）を数値で指定|
|-A ユーザー名:パスワード	|ベーシック認証が必要なコンテンツにテストする|
|-P ユーザー名:パスワード	|認証の必要なプロキシを通じてテストする|
|-X プロキシサーバ名:ポート番号	|プロキシ経由でリクエストする場合に指定|
|-V	|バージョンを表示|
|-h	|ヘルプを表示|

#### 使用法

隣の人のマシンのIPアドレスを調べる


```bash
ab -n 10000 -c 100 http://隣の人のIPアドレス
```

* Complete requestsが正常に処理したリクエスト数
* Failed requestsは、処理に失敗したリクエスト数

* 何リクエストまで耐えられるか
	* Failed requests: を見る
	
	
	-n と -cの値を増やしていく


* 秒間どれくらいのリクエストをさばけるか？
	* Requests per second　を見る

* パフォーマンス
	* Time per request: を見る

## ping による速度測定

* pingコマンドの主なオプション

|オプション 引数	|意味|
|:--|:--|
|-c 数	|パケットの送信回数を指定する|
|-i 秒	|パケットの送信間隔を秒単位で指定する|
|-n	|数値のみ出力する（名前解決を行わない）|
|-r	|ホストへ直接パケットを送信する（ルーティングしない）|
|-R	|パケットの経路を表示する|
|-q	|コマンド実行開始時と終了時のメッセージのみを表示します。|
|-s サイズ	|パケットサイズをバイト単位で指定する（初期値は56）|
|-t TTL値	|パケットのTTL（Time to Live）値を指定する|
|-v	|詳細情報を表示する|

```bash
ping -c 5 -s 1400 -i 0.5 157.13.1.1
```

パケットサイズはフラグメントを起こさないサイズでないとTTLが測定できない


## iperf3 

* サーバとクライアントで測定する
* グループ内で互いのIPアドレスを確認する

#### サーバ側

```bash
iperf3 -s
```

#### クライアント側

```bash
iperf3 -c 
```

* Latency
	* コンピューターにデータ転送などを要求し、その結果が送信されるまでにかかる時間
* Jitter(ジッター)
	* (伝送遅延時間)の変動値
* RTT（ラウンドトリップタイム）
	* 往復時間のこと
* Packet Loss(パケットロス)
	* 通信経路上でデータパケットが喪失し、宛先まで届かないこと


[https://sourceforge.net/speedtest/](https://sourceforge.net/speedtest/)

## munin



