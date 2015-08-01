# ビッグデータ x クラウド

# Googleが描くMapReduceを超えたビックデータの世界

現状 検索インデックス 100PB

* 2002 GFS
* 2004 MapReduce(論文公開) -> Apache Hadoop
* 2008 Dremel
* 2010 Flume
* 2014 MillWheel

Dremel -> Bigquery
Flume+MillWheel -> Cloud Dataflow

## Google Bigquery

* クエリ専用のデータベース(アプリケーションのログなどの分析を実施、リードオンリー)
+ プログラマー以外の人(マーケット、データアナリスト)が使う場合も多い
* 社内のログの解析はBigqueryで実施

### 何故速いか

* カラム型データベース
* 一つのクエリを数千台のサーバで実行する
* セル単位=1万台のサーバ
  * コンテナベースのアプリケーションが各サーバで薄く広く実行

## 使われている場所

* 7&i

# CortanaさんがAzureとやってくる

## Windows 10

## Power Bi

## 実行例

### コカコーラ

自販機 -> Event Hub -> Stream Analytics -> Data Lake
                                        -> Power Bi
### Stream Analytics

データをリアルタイムで解析

### Azure Data Lake Service

### Cortana Analytics Suite

aaa

# AWS Lambda がもたらすデータ処理の自動化とコモディティ化

## AWS概要

2014は518の新機能を追加

## AWS Lambda

アップロードした関数をイベントドリブンに呼び出してくれるサービス

* インフラの管理が不要
  −> ビジネスロジックに注力できる
+ 穏やかな料金体系->100ms単位

### 実施例

+ 画像がアップロードされたタイミングでサムネイルを生成するアプリケーション
* DynamoDBへの書き込みに応じて値チェックをしつつ別テーブルにプッシュ通知を実行

### 例

Server -> Kinesis -> Consumer -> S3 -> Redshift
                                    -> Amazon Elastic MapReduce

_データフローには多くのIf - Thenが生じる_

#### これまでは

監視するアプリケーション等を監視する必要があり、大変
-> _多くIf-ThenはLambdaで代用できる_

### ビックデータ + AWS

AWSのサービス間を結合させる糊みたいな役割ができる

### Lambdaを使った実施例

#### パイプラインのオーケストレーション

* データが来たらDynamoDBに投げる
* データが集まったら、EMRに解析を依頼

#### IoT(TempTracker)

## まとめ

Lambdaを使うことでイベント駆動のサービスを簡単に実装できる。

# Treasure Dataの作り方

+ Fluentd
* MessagePack

## Plazma

+ 45B/day のストリーミング
+ 10B/day のバルク
* Hive 3T/day
  Presto 3T/day

### リソース管理

* Guaranttee : 最低限のリソース
* Boost : 共有の余っているリソースを使用

### Streaming Import
```
Fluentd -> MessagePack -> API Server -> Import Queue -> Import worker

Import Worker -> Real-time storage
時間がたったら
Realtime storage -> Archive Storage
```

* Realtime storageとArchive StorageはDBフォーマットが異なる。
QueneはRealtime storageとArchive Storageの二つに投げる

#### Fluentd

* ログコレクター
* ログにIDを振ることでログの重複を避ける

#### Import Queue

# 質問

## データの蓄積は当たり前だけど、それ以後は?

AWS : データの流速はより速くなるので、データの解析結果をまとめて通知するような仕組み
MicroSoft : 機械学習
Google : 一つのプログラミングでリアルタイムとバッチ処理をおこなえるようにする。機械学習, Deep learning

## データの一貫性などなど

Google : BigQueryについては10年近く前から社内で使っているので、その辺問題は解決済みとの考え
AWS : 既存の仕組みは変わらず、新しい機能は別の機能として追加していくような形
