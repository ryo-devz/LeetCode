# 問題文
https://leetcode.com/problems/two-sum/description/

言語: Python

# Step1

かかった時間：15min

思考ログ：
- 問題を理解する。
  - 配列numsと数値targetが与えられる。配列から取り出した2つの要素の合計がtargetとなるような配列のindexを返す問題
    - 配列の要素は2つ以上
    - 有効な答えは必ず存在する
- どのような解き方ができるか
  - 愚直に配列をループさせて和がtargetとなる要素のindexを返せばいけそう
  - 2つのループを用意する。iは0~n-1、jは1~nまで回す
- Pythonの使い方についてもおさらいしておく
  - for
    - https://www.w3schools.com/python/python_for_loops.asp
  - range：The range() function returns a sequence of numbers, starting from 0 by default, and increments by 1 (by default), and stops before a specified number.
    - https://www.w3schools.com/python/ref_func_range.asp
  - len：Return the number of items in a list
    - https://www.w3schools.com/python/ref_func_len.asp
  
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        ans = []
        for i in range(len(nums)-1):
            for j in range(i+1, len(nums)):
                if nums[i] + nums[j] == target:
                    ans = [i,j]
                    return ans
        return ans
```
疑問点：
- 時間計算量をさらに減らすことは可能なのか？
- 他のアプローチで解くことは可能？
- 返却する変数の命名は妥当？
- ```ans```変数を定義せずに```return```することもできるがどちらが良さそうか
  - 定義する場合は、その変数を使いまわすことが可能だが、今回は特に不要そう
  - 定義しない場合は行数を減らすことができる

参考リンク
- 

# Step2
かかった時間：30min

思考ログ
- まずは過去に実装している人の解き方をいくつか確認してみる
  - 解法について
    - 2重ループせずにhashmapを利用する方法
    - 値とindexのペアをhashmapに保持する
    - hashmapをループして```target```と値の差を取り、hashmapに存在する場合はループ時のindexとhashmapのindexを返す
    - 存在しない場合はhashmapに追加する
  - その他
    - 利用する言語を明記した方が良さそう
    - 時間計算量や空間計算量を意識できていなかった
- 上記踏まえもう少し深掘りして理解を深める
  - hashmapとは？
    - キーと値を組み合わせたdictionary（辞書）
    - 値とindexを持たせることで解くことが出来そう
  - 時間計算量（Time Complexity）とは？
    - ```「プログラムの実行に必要な計算のステップ数が入力に対してどのように変化するか」という指標を時間計算量といいます。 計算ステップ数とは、四則演算や数値の比較などの回数です。```
    - 2重ループはO(n^2)、1重のループはO(n)、ループすることがないような処理はO(1)、分割して探索するアルゴリズムを利用する際はO(logN)といった計算量になる
  - 空間計算量（Space Complexity）とは？
    - ```「プログラムの実行に必要なメモリの量が入力に対してどのように変化するか」という指標を空間計算量といいます。```
    - 2次元配列はO(n^2)、1次元配列はO(n)、変数の格納のみの場合はO(1)といった計算量になる
    - https://atcoder.jp/contests/apg4b/tasks/APG4b_w?lang=ja
    - 時間計算量と空間計算量はLeetCodeの```submit```後の実行結果から確認できるので答え合わせに良さそう。（```Runtime```や```Memory```の```Analyze Complexity```）※プレミアムに加入が必要なのか・・・
  - enumerateとは？
    - indexと要素を返してくれる関数。hashmapのループに利用できそう。
    - https://docs.python.org/3/library/functions.html#enumerate

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        pair_index = {}
        for i, num in enumerate(nums):
            if target - num in pair_index:
                return [i, pair_index[target - num]]
            pair_index[num] = i
```

# Step3
かかった時間： 5min

上記を書き直し、実装。

思考ログ
- numsとnumが似ているのは混同する可能性があるので他の命名にした方が良さそう？
- pair_indexは分かりやすい名前なのか？
- 有効な答えは必ず存在するという前提からループを抜けてからのreturnは不要と判断

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        pair_index = {}
        for i, num in enumerate(nums):
            if target - num in pair_index:
                return [i, pair_index[target - num]]
            pair_index[num] = i
```

# Step 4 
- レビューを持って修正を行う

```python


```
