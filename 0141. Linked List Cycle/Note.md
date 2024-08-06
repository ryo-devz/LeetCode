# 問題文
https://leetcode.com/problems/linked-list-cycle/description/

# Step1

かかった時間：10min

思考ログ：
- 問題を理解する。
  - Linked Listが与えられて、サイクル（循環）が存在するかを判定する問題。

- どのような解き方ができそうか。
  - Linked Listをループさせて、要素に印をつけていき、印のある要素が再度出現した場合はTrueを、ループを抜けてしまった場合はFalseを返す方法でいけそう。

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        if head is None or head.next is None:
            return False
        while head:
            if head.val == "*":
                return True
            head.val = "*"
            head = head.next
        return False
        
```
疑問点：
- Linked Listとは？
  - ノードの値と次の要素の参照を持っているデータの構造体。配列と比較してデータの挿入と削除が可能。
- 'pos'とは？
  - 循環の始まりのindexを表す。-1の場合、循環しない扱いとなる。
- 引数のLinked Listが書き換わってしまうので、変更せず解く方法はないか。
 
参考リンク
- Linked List
  - https://www.geeksforgeeks.org/linked-list-data-structure/
 
# Step2
かかった時間：15min

思考ログ
- その他の解き方が無いか調べてみる。
  - フロイドの循環検出法というもので対応できそう
  - 速く動く、遅く動く2つのインデックスを利用して循環を検出するアルゴリズム
  - https://ja.wikipedia.org/wiki/%E3%83%95%E3%83%AD%E3%82%A4%E3%83%89%E3%81%AE%E5%BE%AA%E7%92%B0%E6%A4%9C%E5%87%BA%E6%B3%95

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        if head is None or head.next is None:
            return False
        slow = fast = head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            if slow == fast:
                return True
        return False
```

# Step3
かかった時間： 5min

上記を書き直し、実装。

- 1行目のif文はwhile文の条件と重複しているため破棄。

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        slow = fast = head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            if slow == fast:
                return True
        return False
```

# Step 4 
- レビューを依頼して修正を行う

```python


```
