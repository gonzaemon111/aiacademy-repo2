# Pandasについて

## Pandasとは

Pandas(パンダス)は**データ解析を容易にする機能を提供するPythonのデータ解析ライブラリ**です。
Pandasの特徴には、データフレーム(DataFrame)などの独自のデータ構造が提供されており、様々な処理が可能です。
特に、表形式のデータをSQLまたはRのように操作することが可能で、かつ高速で処理出来ます。
最新情報に関しては 公式ドキュメントを参考してください。

さて、Pandasを使うことで何ができるのでしょうか？
例えば、Pandasでは下記のようなことが出来ます。

```txt
    CSVやExcel、RDBなどにデータを入出力できる
    データ前処理(NaN / Not a Number、欠損値)
    データの結合や部分的な取り出しやピボッド(pivot)処理
    データの集約及びグループ演算
    データに対しての統計処理及び回帰処理
```

## なぜPandasを学ぶのか

なぜPandasを学ぶのかについて説明します。
**機械学習においてデータの前処理は多くの時間を割くことになりますが、Pandasを使うことでこのデータの前処理という工程を効率よく行うことが出来ます。**
機械学習エンジニアやデータサイエンティストがPythonでデータの前処理をする上で必要なPandasをこの章では説明していきます。

## Pandasを使うメリット

Pandasを使うメリットは主に2つあります。
**1. 多種の型のデータを一つのデータフレームで扱えること**
NumPyの配列（np.array）はすべての要素が同じ型でなければなりません。
よって、csvファイルの読み書きなどでは、NumPyは非常に不便なライブラリです。
その点、Pandasのデータフレームは異なる型のデータを入れることが出来ます。
Pandasのデータフレームに格納することで、データの前処理が容易にできます。
**2.データ加工や解析の関数が多いこと**
別章で示した欠損値の削除・補完の他にも、これから紹介する様々な便利な関数がPandasには備わっています。
そういった様々な関数の使い方をこの章では学びます。

## データ型(pandasの基本データ型)

PandasはNumPyをベースとして構築されているため、NumPyのndarrayとの相性が良いです。
2つのデータ型でデータを保持します。

1.シリーズ(Series)
2.データフレーム(DataFrame)

1つ1つ見ていきましょう。

## シリーズ

Seriesは1列のみのデータ型です。

```python
import pandas as pd
# from pandas import Series

s1 = pd.Series([1,2,3,5])
print(s1)

"""
# 左の列は行ラベル
" 右の列はシリーズのデータ
0    1
1    2
2    3
3    5
dtype: int64 # データの型
"""
```

**シリーズはデータ(values)とそれに対応する行ラベル(index)を持つ1次元データ構造であり、辞書型とは違ってデータには順番があります。**


## データフレーム

データフレームは**2次元のラベル付きのデータ構造で、Pandasでは最も多く使われるデータ型**です。
データフレームのイメージとして、スプレッドシートやSQLのテーブルをイメージするとわかりやすいです。
DataFrameは複数の列を持ち、DataFrameから1列を抽出した場合も勝手にSeriesになります。
また、シリーズと同様に様々な型のデータを保持することが出来ます。

```python
import pandas as pd
df = pd.DataFrame({
    '名前' :['田中', '山田', '高橋'],
    '役割' : ['営業部長', '広報部', '技術責任者'],
    '身長' : [178, 173, 169]
    })
print(df)
print(df.dtypes)

print(df.columns) # 列ラベルの確認(辞書型のkeyが列ラベル）
```

データフレームは、リスト型のデータを持つ辞書型をDataFrame関数の引数に渡すことで、データフレームを生成することが出来ます。
保持されるデータの列の順序ですが、列ラベルによって自動的にソートされます。
ですので、データを与えた時点での順序と異なってしまう可能性があるので注意です。
ですが、columns引数に列の順序を指定することでその通りに作成可能です。


```python
import pandas as pd
data = {
    '名前' :['田中', '山田', '高橋'],
    '役割' : ['営業部長', '広報部', '技術責任者'],
    '身長' : [178, 173, 169]
    }
df = pd.DataFrame(data, columns=["名前", "役割", "身長"]) # データフレーム生成時に対応するデータを持っていない場合、そのデータの列にはNaNが割り当てられます。
# また下記のようにすることで、カラムの名称を変更・置換可能です
df.columns = ["Name", "Position", "height"]
print(df)
```

## 条件による行の抽出(query)

`query`を利用することで`pandas.DataFrame`の列の値に対し、条件に応じて行を抽出することが可能です。
比較演算子を利用した複数の条件指定が出来ます。

```python
import pandas as pd
df = pd.DataFrame([[10, 20,30, 30], [25, 50,65, 80]], index=["1行", "2行"], columns=["A", "B", "C", "D"])
print(df)
#       A   B   C   D
# 1行  10  20  30  30
# 2行  25  50  65  80

print(df.query('A >= 5 and C <= 50'))

#      A   B   C   D
# 1行  10  20  30  30
```
上記プログラムは、A列が5以上かつ、C列が50より小さい値が含まれている行を抽出するプログラムです。

## データの入出力

Pandasはデータをファイルから入力及び解析後のデータをファイルを出力する機能があります。
Pandasでは大きく4つの入出力が可能です。

1. テキスト形式のデータファイルからデータの読み込み
2. バイナリ形式のデータファイルからデータの読み込み
3. データベースからのデータの読み込み
4. Web上からのデータの読み込み

例えば、Pandasでcsvファイルを読み込む場合は、「read_csv」を使い、データの出力には「to_csv」や「to_excel」などが利用可能です。csv以外にも、「read_json」や「read_excel」、「read_json」「read_sql」もあり、それらの出力メソッドもあります。
TSVファイルの場合は、「read_table」を使うことで区切り文字がタブ\tのファイルを処理することが出来ます。
試しにcsvファイルを読み込んでみましょう。

## Pandasソート

**インデックス (行名・列名)を使う方法と値に基づいてソートする方法があります。**
`.sort_index()`を使うことで、インデックス（カラム名、行名）に基づいてソートを行うことができます。
そのまま使うと、昇順（小さい順）でのソートとなりますが、引数に、`ascending=False`を記述することで降順(大きい順)のソートができます。
`.sort_values(by=カラムのリスト)`を使うことで、列の値の小さい順にソートすることができます。

```python
import pandas as pd
import numpy as np
df = pd.DataFrame(np.random.randn(20,2))
df.sort_index(ascending=False) # 降順

# 昇順でソートするには上記の降順ソートのコードをコメントアウトして下記を実行してください
df.sort_values(by=1) # key(カラム名)が1の昇順(小さい順)でソート
df.sort_values(by=1, ascending=False)  # keyが1の降順(大きい順)でソート
```
上記を実行すると次のように出力されます。
（random.randn()を用いているため、実行ごとによって出力が変わります。）

## 欠損値の処理

Pandasには欠損値(NaN)の扱うメソッドは「`dropna`」、「`fillna`」、「`isnull`」、「`notnull`」があります。
1つ1つ解説していきます。
まず**dropnaは指定の軸方向にデータ列を見て、欠損値(NaN)の有無に関して指定の条件を満たす場合に、そのデータ列を削除します。**
fillnaは欠損値を指定の値もしくは、指定の方法で埋めることができます。
isnullはデータの要素ごとにNaNはTrue、それ以外をFalseとして扱い、元のデータと同じサイズのオブジェクトを返します。
notnullはisnullとは逆の真偽値を返します。

```python
import numpy as np
import pandas as pd
df = pd.DataFrame({"int": [1, np.nan, np.nan, 32],
                   "str": ["python", "ai", np.nan, np.nan],
                   "flt": [5.5, 4.2, -1.2, np.nan]})
print(df)

# df成分に対してNaNの地位をTrueとしたブールの値のデータフレームを返す
print(df.isnull()) # notnull()を使うと、TrueとFalseが逆の処理になる。

# "int"列にNaNがある行の削除
print(df.dropna(subset=["int"]))

# NaNがある行を全て削除する
print(df.dropna())

# NaNを全て0に置換する
print(df.fillna(0)) # 第一引数にmethod="ffill" 第二引数にlimtit=数字 とすることで指定した数字までは前のデータを使ってNaNを埋めることができます

df2 = pd.DataFrame({"int": [1, np.nan, np.nan, 32],
                   "str": ["python", "ai", np.nan, np.nan],
                   "flt": [5.5, 4.2, -1.2, np.nan]})

# int列だけ0で補完
df2.fillna({"int": 0}) # 特定の列に対しては辞書型を用いる


# 列ごとに異なる値を使いたい時は複数のキーを渡す。
df2.fillna({"int": 0, "str": "ai"}) 

# 特定の列(例えばflt)を削除
df2.drop(labels="flt",axis=1)
"""
  int str
0 1.0 python
1 NaN ai
2 NaN NaN
3 32.0  NaN
"""

# 複数の列を削除
df2.drop(labels=["flt", "str"],axis=1)

"""
  int
0 1.0
1 NaN
2 NaN
3 32.0
"""

# indexを指定すると行を消すこともできます
df2.drop(index=1, axis=0)
"""
int str flt
0 1.0 python  5.5
2 NaN NaN -1.2
3 32.0  NaN NaN
"""

# 元のデータに反映して削除するにはinplaceオプションにTrueを渡します
df2.drop(labels="flt", axis=1, inplace=True)
print(df2)

"""
int str
0 1.0 python
1 NaN ai
2 NaN NaN
3 32.0  NaN
"""
```
