# Matplotlibについて

Matplotlib は**Pythonのグラフ描画のためのライブラリ**です。
Matplotlibを使うことで、グラフの描画やデータの可視化が簡単に行えます。
折れ線グラフ、ヒストグラムや散布図など表現可能です。
[公式ギャラリー](https://matplotlib.org/gallery.html)にて実際の例を見ることでより理解が深まりますので参考にして頂ければと思います。

## Matplotlibの使い方

Matplotlibを使った最も簡単なグラフの書き方は次の通りです。

1. matplotlib.pyplotをインポートする
2. x軸の配列を作る
3. y軸の配列を作る
3. plot関数を使いプロットする
4. show関数を使いプロットしたグラフを描画する

```python
import numpy as np
import matplotlib.pyplot as plt

x = np.arange(-5, 5, 0.1) #-5から5まで0.1区切りで配列を作る
y = np.sin(x) #配列xの値に関してそれぞれsin(x)を求めてy軸の配列を生成

plt.plot(x,y) # この場合のplot関数の第一引数xは、x軸に対応し、第二引数のyがy軸にあたります。
plt.show()
```

![Matplotlibのsin関数](https://aiacademy.jp/assets/images/plot_1.png)

## 折れ線グラフ

折れ線グラフは、**数量の大きさを表す位置を線で結んだグラフ**です。
時間とともに変化する数量を示すときに利用します。

```python
import matplotlib.pyplot as plt
data = [2, 4, 6, 3, 5, 8, 4, 5]
plt.plot(data)
plt.show()

# r--は赤の点線 b--は青の点線 g-- は緑の点線
plt.plot([1,2,3,4],[1,5,10,15],"r--") # 引数にオプションを渡さずに 色 に -- をつけると色 + 点線で表現できます
plt.show()
```

![折れ線グラフ](https://aiacademy.jp/assets/images/matplotlib_plot.png)

