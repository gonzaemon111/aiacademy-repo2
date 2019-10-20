# AIacademy Numpy Repo

## NumPyとは
NumPy(ナムパイ/ナンパイ / Numerical Python)はPythonで数値計算を効率的に行うためのライブラリで、データ解析及び、線形代数を扱う上では必須のライブラリです。
NumPyを使うことでベクトルや行列などの多次元配列を作ることができます。
NumPyは、Matplotlib、Pandas、SciPyなどのPythonのライブラリと合わせてよく利用されます。
[公式ドキュメント](https://docs.scipy.org/doc/numpy/reference/)


## なぜNumPyを学ぶのか
なぜNumPyを学ぶのかについてあらかじめ説明します。
NumPyは機械学習・ディープラーニングを扱う機械学習エンジニア(Pythonエンジニア)に取って、必須のライブラリといっても良いくらい、多く利用します。
NumPyは大規模なデータの処理に優れており、機械学習・ディープラーニングの現場で多く使います。
そのためNumPyは機械学習エンジニアにとって「最初の一歩」となるライブラリですので、是非この章でしっかり基礎を学んでいきましょう。

## 配列(アレイ)を作る
array()を使うことでNumPyの配列を作ることが出来ます。

```python
import numpy as  np
x = np.array([1.0, 2.0, 3.0, 4.0, 5.0])
print(x)
# array()は、Pythonのリストを渡すことでNumPy 用の配列(numpy.ndarray)を生成します。

x = np.array([1,2,3])
print(x) # [1 2 3]
print(type(x)) # <class 'numpy.ndarray'>

my_list1 = [1,2,3,4,5]
my_array1 = np.array(my_list1) # numpyのarrayを作る

my_list2 = [10,20,30,40,50]
my_lists = [my_list1, my_list2] # リストのリストを作る。
my_lists # [[1, 2, 3, 4, 5], [10, 20, 30, 40, 50]] # リストのリストが完成。

# my_listsを使ってNumPyのアレイを使る。（多次元配列を作る）
my_array2 = np.array(my_lists)

my_array2 # 2行5列の配列ができる。
"""
array([[ 1,  2,  3,  4,  5],
       [10, 20, 30, 40, 50]])
"""

# 次のように、タプルを複数渡すとエラーになってしまいます。
np.array((1,2,3),(4,5,6))

"""
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: data type not understood
"""

```

## NumPy配列の形状を調べる
NumPy配列(ndarray)の形状を調べるにはshapeというインスタンス変数を使うことで調べることができます。
※インスタンス変数とはオブジェクトのインスタンスごとに割り当てられた変数のこと(個々のインスタンスに格納される変数)です。
詳しくは、クラスとオブジェクトのテキストをご確認ください。

```python
import numpy as np
a = np.array([1, 2, 3, 4])
a.shape # (4,)が出力される。これは1次元配列でかつ、4つ要素があることを意味します。

b = np.array([[1, 2],[3,4]])
b.shape # (2, 2) これは行列で、2行2列を意味しています。
```


## 配列の生成 arange()

arange()はpythonのfor文で使ったrange()関数と似た関数です。
range()同様に引数に渡した数の配列を生成します。

```python
import numpy as  np
# データの準備
# 等間隔の数字
# 0から9までの数字(配列)を生成
x = np.arange(10)
print(x)

# reshape()は配列を形状に変換します
x = np.arange(1, 10).reshape(3,3) # 3×3の多次元配列に変換
y = np.arange(1, 10).reshape(3,3) # 3×3の多次元配列に変換
"""
xを下記のように書き換えることも可能
x = np.reshape(x, (3,3))
"""
print(x)
print(y)

print(x + y)
print(x - y)
print(x * y)
```

`reshape(x,y)`メソッドで、x×yの多次元配列の生成が可能

## 配列操作

NumPyでは再形成といって、配列の次元を変更することが可能です。

```python
import numpy as np
sample_array = np.arange(10)
print(sample_array)

# reshapeを使って配列の形状を指定
sample_array2 = sample_array.reshape(2,5)
print(sample_array2) #array(([0,1,2,3,4],[5,6,7,8,9]])

# concatenateを使って、データの結合する(axisで行方向か、縦方向を指定可能)
sample_array3 = np.array([[1,2,3],[4,5,6]])
sample_array4 = np.array([[7,8,9],[10,11,12]])

# 行方向に結合 ([[1,2,3,7,8,9],4,5,6,10,11,12]])
print(np.concatenate([sample_array3,sample_array4],axis=1))

# hstackでも行方向の結合が可能
print(np.hstack((sample_array3,sample_array4)))



"""
axis=0で列方向
axis=1で行方向です。
下記URLを参考ください。
https://qiita.com/shuetsu@github/items/2bf8bba233c5ecc7a0ad
"""

# axisに0を設定しているので、列方向 ([[1,2,3],[4,5,6],[7,8,9],[10,11,12]])
print(np.concatenate([sample_array3,sample_array4],axis=0))

# vstackで列方向の結合が可能
print(np.vstack((sample_array3,sample_array4)))
```

## ブロードキャスト

ブロードキャストは、配列の大きさが異なっていれば、自動的に要素をコピーし大きさを揃えるNumPyの機能です。

```python
import numpy as np
# データの準備
sample_array = np.arange(10)
print(sample_array)

# 上記の配列に「5」を足す計算
# 要素をコピーして大きさを揃えて、配列の全ての要素に5を加算
print(sample_array + 5)
```

![ブロードキャストの説明図](https://camo.qiitausercontent.com/bd16245d17b1cbfaa7a9f267de2d8dae8ef39cec/68747470733a2f2f71696974612d696d6167652d73746f72652e73332e616d617a6f6e6177732e636f6d2f302f3137313731352f65393664663264642d353937342d353662312d313239652d3236373162383062343535642e706e67)

