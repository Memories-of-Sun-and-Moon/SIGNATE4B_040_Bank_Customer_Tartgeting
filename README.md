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

```text
   id  age           job  marital  education default  balance  ... month duration campaign  pdays previous  poutcome  y
0   0   31      services  married  secondary      no    12294  ...   nov      101        3    498        0     other  0
1   1   29  entrepreneur   single   tertiary      no    43027  ...   aug      158        2    702        0   unknown  1
2   2   35    management  married   tertiary      no    12252  ...   nov      351        1    826        0   failure  0
3   3   31    technician  married  secondary      no    99121  ...   may      658        2    120        0   failure  0
4   4   48    unemployed  married    primary      no    42005  ...   apr      177        1    273        0   unknown  0
```

![train.csvの説明](picture/train_explain.png)

### 投稿用ファイル (submit_sample.csv)