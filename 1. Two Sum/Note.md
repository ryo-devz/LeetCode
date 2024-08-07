# 問題文
https://leetcode.com/problems/two-sum/description/

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
参考リンク
- 
# Step2
かかった時間：XXmin

思考ログ
- XXX

```python

```

- XXX
```python

```

# Step3
かかった時間： XXmin

上記を書き直し、実装。

```python

```

# Step 4 
- レビューを持って修正を行う

```python


```
