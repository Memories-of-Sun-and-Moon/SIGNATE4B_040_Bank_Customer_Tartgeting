# MEMO

## python の開発環境に入る時に必要なコマンド

```sh
source env/bin/activate
```

# 【第40回_Beginner限定コンペ】銀行の顧客ターゲティング

顧客の属性情報などから定期預金キャンペーンの反応率を予測しよう。

## 今回のテーマ
顧客属性データおよび、過去のキャンペーンでの接触情報に基づいて口座を開設したかを予測するモデルの構築
※本テーマ設定は練習問題に掲載のタスクと同様ですが、データは異なるものを使用しております。

## データ

### 学習用データ (train.csv)
### テスト用データ (test.csv)

| |id|age|job|marital|education|default|balance|housing|loan|contact|day|month|duration|campaign|pdays|previous|poutcome|y|
|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|
|0|0|31|services|married|secondary|no|12294|yes|no|cellular|21|nov|101|3|498|0|other|0|
|1|1|29|entrepreneur|single|tertiary|no|43027|no|no|cellular|22|aug|158|2|702|0|unknown|1|
|2|2|35|management|married|tertiary|no|12252|yes|no|cellular|11|nov|351|1|826|0|failure|0|
|3|3|31|technician|married|secondary|no|99121|yes|yes|unknown|16|may|658|2|120|0|failure|0|
|4|4|48|unemployed|married|primary|no|42005|yes|no|telephone|3|apr|177|1|273|0|unknown|0|

[変換ツール](https://markdown-convert.com/ja/tool/table)

```python
job = ['services' 'entrepreneur' 'management' 'technician' 'unemployed' 'blue-collar' 'admin.' 'retired' 'self-employed' 'housemaid' 'student']
marital = ['married' 'single' 'divorced']
education = ['secondary' 'tertiary' 'primary' 'unknown']
default = ['no' 'yes']
housing = ['yes' 'no']
loan = ['no' 'yes']
contact = ['cellular' 'unknown' 'telephone']
month = ['nov' 'aug' 'may' 'apr' 'sep' 'jun' 'jul' 'feb' 'oct' 'jan' 'mar']
poutcome = ['other' 'unknown' 'failure' 'success']
```

![train.csvの説明](picture/train_explain.png)

train.csvには $y$ の結果がない

![可視化のリンク](https://qiita.com/TaigoKuriyama/items/fccc5dd31326051d1d19) を見ながら異論値を可視化してみたり、検証してみたりしている。

```sh
27100 rows and 18 features in train set
18050 rows and 17 features in test set
```

欠損値は存在しなかった。


| |id|age|balance|day|duration|campaign|pdays|previous|y|
|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|
|count|27100.000000|27100.000000|27100.000000|27100.000000|27100.000000|27100.000000|27100.000000|27100.000000|27100.000000|
|mean|13549.500000|36.073284|47682.901771|16.747528|229.325387|1.775830|432.482399|0.085720|0.077934|
|std|7823.240484|7.816417|31650.760036|8.569529|204.939958|0.950045|252.150648|0.365889|0.268072|
|min|0.000000|22.000000|-6847.000000|1.000000|0.000000|1.000000|-1.000000|0.000000|0.000000|
|25%|6774.750000|31.000000|20015.750000|8.000000|121.000000|1.000000|214.000000|0.000000|0.000000|
|50%|13549.500000|33.000000|47624.000000|17.000000|158.000000|1.000000|432.000000|0.000000|0.000000|
|75%|20324.250000|37.000000|75330.000000|26.000000|345.000000|2.000000|650.000000|0.000000|0.000000|
|max|27099.000000|90.000000|102121.000000|31.000000|3076.000000|5.000000|870.000000|3.000000|1.000000|

- pdaysが負の値を取ることはあるのだろうか

### 投稿用ファイル (submit_sample.csv)

| |0|0.1|
|:----|:----|:----|
|0|1|0|
|1|2|0|
|2|3|0|
|3|4|0|
|4|5|0|

$1$ か $0$ かを出せばいいことを行っているだけのサンプル

# 日記

## 11/22

JOIN

kaggleスタートブックの最初の提出と同じようなものを作った。

ウエイトが偏っているものが多く、そのままだと全員が $0$ となってしまった。

それを改善するために ``balanced`` をしたけれど、今度は $1$ が過剰な量になってしまう。難しいね。