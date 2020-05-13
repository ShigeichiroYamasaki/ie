# AWS Educate の使い方

## AWS Educateとは？ 
AWS Educateは、誰でも自由に参加できるクラウド学習プログラム。(14歳以上の学生もしくは教員が参加可能)


* 近畿大学はAWS Educate加盟校です
* 登録にクレジットカードが不要です
* インターネット工学演習は、Amazon のクラウドサービス Amazon EC2 を利用します

## AWS Educate2つの方法

*  自身のAWSアカウント(事前に作成してあるもの)を使用して、AWS Educateを使用する。
登録には、クレジットカードを必要とするが、AWS サービスは自由に使用でき、AWS Educate のプロモーションクレジットがなくなってもアカウントのリソースは維持される。

*  AWS Educate Starterアカウントを新規作成して使用する。
無料のAWS Educateプロモーションクレジットがすでにアカウントで使用可能であるため、Starterアカウントを使用するのにクレジットカードは必要ない。

## AWS Educateアカウント作成の流れ

[https://aws.amazon.com/jp/education/awseducate/](https://aws.amazon.com/jp/education/awseducate/)

### ステップ 1/3: 役職を選択します

学生

### ステップ 2/3: お客様の情報を入力します

* Kindai University
* Japan
* メールアドレス

「私はロボットではありません」にチェックを入れる

### 利用規約画面にて同意をするとサンクスページが表示

このタイミングではまだ申請は完了していない

### 申請画面で入力されたメールを確認

メール中のリンクをクリックすることで申請完了


## AWS Educate ポータルの利用

### AWS Educate Application Approved メール

* 承認されると、メールが届く

その中のリンクをクリック「click here」


### 承認後の初回ログイン

* 右上のオレンジ色のボタン「Sign In to the console」をクリック

*  IAM ユーザー

パスワード

## ソリューションの構築

### 仮想マシンを起動する

#### ステップ 1: Amazon マシンイメージ (AMI)

* 無料利用枠のもののみ

* Ubuntu Server 18.04 LTS (HVM), SSD Volume Type - ami-0278fe6949f6b1a06 (64 ビット x86) / ami-039202b3bbbe96f2d (64 ビット Arm)

「選択」

#### ステップ 2: インスタンスタイプの選択

「確認と作成」

#### ステップ 7: インスタンス作成の確認

## ssh で接続する１

[https://docs.aws.amazon.com/ja_jp/AWSEC2/latest/UserGuide/ec2-instance-connect-set-up.html#ec2-instance-connect-setup-security-group](https://docs.aws.amazon.com/ja_jp/AWSEC2/latest/UserGuide/ec2-instance-connect-set-up.html#ec2-instance-connect-setup-security-group)

鍵の名前などが異なる

```bash
ssh -i "yamasaki.pem" ubuntu@ec2-13-231-108-8.ap-northeast-1.compute.amazonaws.com
```

```bash
 sudo apt-get update
 ```
 
 ```bash
 sudo apt-get install ec2-instance-connect
 ```
 