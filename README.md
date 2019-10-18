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