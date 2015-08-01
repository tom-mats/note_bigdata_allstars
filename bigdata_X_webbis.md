# ビッグデータ x ウェブビジネス

# ビックデータとウェブビジネス

## データで見るYahoo. Japan

略

## サーチビジネスを支えるライブテストの裏側

* 一つのテストにかかる時間 2週間
* テストの本数 40本
* 分析指標 50
* 採用率 30%
* 対象 数千万人

### テスト管理

+ 同時期に数十案件
* ユーザ行動を考えたテスト期間
  * 大型連休とかは無視
+ デバイスごとにテスト設計
  * AndroidとiPhoneですら分けている。

### サービス間連携テスト

* 検索とショッピング等の連携
+ サービス単体だけでなく全体を最適化

### テスト効率化

* マルチレイヤー化
  * Online controllerd experimentast lage scale : Microsoft
  * Overlapping experiment infrastrure more better faster experimentation : Google

## DMPの仕組み

* 自社データYahooのビックデータを組み合わせて解析

### DMPで消費者分析=競合を知るという使い方

### システム概要

* データのストア先はHadoop (4000台)
* SolrCloud 3クラスタ

* Audience に Ads, DMP, 検索等の情報をまとめる
* AudienceからSolrCloudクラスタに書き込む

# グローバル化、多様化するウェブサービスに対峙する分析環境

## 分析プラットフォーム

### 分析の対象

* Collecting: データの集約 fluentd, Hadoop
* Reporting: サービスの状況報告 Hive, shib norikra, cognos pentaho, kibana
* Analyizing: Presto infiniDB

### LINEの中の様々なサービスのデータ集計や可視化をサポート

```
Server -> Fluentd -> Data Lake(Hadoop) -> Query UI
                  -> Realtime Analyizing -> DashboardやNotification

Data Lake -> HDFS(Hive, Presto) Hive -> ETL -> DWH(InfinDB)

Bi Tool -> Presto
        -> DWH
```

### BIツール Cognos

* IBM社製のレポートオーサリングソフト
* 200レポートぐらい
* 認証, DB接続は独自

### BIツール Pentaho

* OLAP型の多次元分析用システム
  * カテゴリ別
  * アイテム別
などの分析を実施

###  BIツール Kibana

* リアルタイムデータの可視化に利用

## 課題と解決

### 問題点

* KPIが激増
  * 国別
  * カテゴリ別
  * サービスとの連携
  * xxかつyyの条件で
  * 意味不明な要望
->
たくさんありすぎて、誰もデータ見なくなる

### 解決策

KPIモニタリング
* KPIを自動評価して、異常な状態を通知する。

#### 技術要件

* 統計モデル、機械学習の処理系を組み入れられる
* 分散処理ができる

#### システム
