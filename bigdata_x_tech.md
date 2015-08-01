# ビックデータxウェブ事業を支える技術

# 検索基盤Qass

## Qassとは

* EleasticSearch を軸とした検索サービス

## 検索品質とは

* 再現率 ユーザ求めていた情報が検索結果に含まれていた割合
* 適合率 検索結果のなかにユーザが求めていた情報の割合
の両方を上げるべきだが、相反しあう指標

### 再現率の向上

* 形態素辞書の拡充
* クエリ展開

### 適合率

* 正規化
* 表記ゆれ
* 同義語、略語

## ライブイベントにおける「見る」検索

* 情報誌に近い

### 施策

+ 編集者のKKD(かん、経験、度胸)をモデル化
  * 検索結果のランキングに反映

# Spark機械学習

Apache sparkを使ったCTR推定

```
csv -> spark->cv 特徴ベクトルに変換 -> 学習 -> 検証
```

## 使うもの

Apache spark
* SparkSQL
* Spark MLlib
  * Pipeline
  * ...

## Spark-csv

ヘッダとカラムが対応したDataFrameを生成できる

## 特徴ベクトル

目的変数(Click/non click)を説明変数(その他)に分けるようにする

## 学習

Pipelineを使ってHashingTrickによる特徴のベクトル化-ロジスティック回帰

## 検証

交差検証用のライブラリがSpark MLlib二存在する。

# Spark streamingと Spark Graph Xを利用したTwitter解析

## 目的

* ストリーミング処理でTwitterオンライン解析がした
* Scalaの知見
* 検証用のマイクロサービスの適用


## Spark streaming
