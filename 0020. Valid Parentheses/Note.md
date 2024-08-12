# 問題概要
問題: 20. Valid Parentheses

https://leetcode.com/problems/valid-parentheses/description/

言語: Python

# Step1

かかった時間：30min

思考ログ：
- 問題を理解する。
  - 3種類の括弧が含まれる文字列が与えられ、括弧が正しく閉じられているか判定する問題と理解
  - その他の制約など
    - 開き括弧は同じ種類の括弧で閉じられなけらばならない
    - 開き括弧は正しい順で閉じなけらばならない
    - 全ての閉じ括弧は同じ種類の開き括弧を持たなければならない
    - 文字列は```'()[]{}'```のみを含む
- どのような方法で解けそうか？
  - Stackを使って括弧が閉じたものから消し込んでいけば実現できそう
  - 開始括弧溜めていき、閉じ括弧が来たら対応する開始括弧を消し込んでいく
  - 対応するものがなければその時点でFalse,全ての括弧が消し込めればTure、そうでなければFalse
- stackとは？
  ```
  A stack is a linear data structure that follows the Last In, First Out (LIFO) principle.
  This means that the last element added to the stack is the first one to be removed.
  It can be visualized as a pile of plates where you can only add or remove the top plate.
  ```
  https://www.geeksforgeeks.org/difference-between-stack-and-queue-data-structures/
- queueとは？
  ```
  A queue is a linear data structure that follows the First In, First Out (FIFO) principle.
  This means that the first element added to the queue is the first one to be removed.
  It can be visualized as a line of people waiting for a service, where the first person in line is the first to be served.
  ```
  https://www.geeksforgeeks.org/difference-between-stack-and-queue-data-structures/

- listやDequewoを利用して実現できそう
- https://www.geeksforgeeks.org/stack-and-queues-in-python/
1) Using list
  - Stack
    ```python
    # Python code to demonstrate Implementing  
    # stack using list 
    stack = ["Amar", "Akbar", "Anthony"] 
    stack.append("Ram") 
    stack.append("Iqbal") 
    print(stack) 
      
    # Removes the last item 
    print(stack.pop()) 
      
    print(stack) 
      
    # Removes the last item 
    print(stack.pop()) 
      
    print(stack) 
    ```
    - ```append```で後ろに追加される
    - ```pop```で後ろの要素から削除される
  - Queues 
    ```python
    # Python code to demonstrate Implementing  
    # Queue using list 
    queue = ["Amar", "Akbar", "Anthony"] 
    queue.append("Ram") 
    queue.append("Iqbal") 
    print(queue) 
      
    # Removes the first item 
    print(queue.pop(0)) 
      
    print(queue) 
    # Removes the first item 
    print(queue.pop(0)) 
    print(queue) 
    ```
    - ```pop```で削除する際にindexを指定する必要がある。
2) Using Deque
  - Stack
    ```python
    # Python code to demonstrate Implementing  
    # Stack using deque 
    from collections import deque 
    queue = deque(["Ram", "Tarun", "Asif", "John"]) 
    print(queue) 
    queue.append("Akbar") 
    print(queue) 
    queue.append("Birbal") 
    print(queue) 
    print(queue.pop())                  
    print(queue.pop())                  
    print(queue) 
    ```
    - ```deque```のimportが必要
    - 宣言時にdequeの記載が必要
    - 基本的にlistと使い方は同じ
  - Queues 
    ```python
    # Python code to demonstrate Implementing  
    # Queue using deque 
    from collections import deque 
    queue = deque(["Ram", "Tarun", "Asif", "John"]) 
    print(queue) 
    queue.append("Akbar") 
    print(queue) 
    queue.append("Birbal") 
    print(queue) 
    print(queue.popleft())                  
    print(queue.popleft())                  
    print(queue) 
    ```
    - ```popleft```で先頭の要素を削除する必要がある。

```python
# 時間計算量：O(n)
# 空間計算量：O(n)
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []
        for bracket in s:
            if bracket == "(" or bracket == "[" or bracket == "{":
                stack.append(bracket)
            else:
                if bracket == ")" and stack[-1] == "(":
                    stack.pop()
                elif bracket == "]" and stack[-1] == "[":
                    stack.pop()
                elif bracket == "}" and stack[-1] == "{":
                    stack.pop()
                else:
                    return False
        if len(stack) != 0:
            return False
        return True
```

疑問点：
- stack[-1]で要素が無かったときにエラーになる？
  
  →yes。初手で")"が来た場合にエラー落ちするので、上記の手法でいくならlen(stack) >= 1で判定する必要がある。
- popで要素が無かったときにエラーになる？
  
  →yes
- if文が同じような構成になっているのでまとめられるか。
- 他の方法で解くことはできないか。少なくともDequeを利用して書き換えることは可能。

参考リンク
- 
# Step2
かかった時間：20min

思考ログ
- 他の方の解き方を参考にしてみる
  - 括弧のペアをMapで管理するのは扱いやすそう。keyが左括弧、対となる閉じ括弧も取得できる。
  - ```pop```した際に値を格納しておけるのか・・・これは利用できそう。
  - ```leftBracket```と```rightBracket```という命名は分かりやすそう。
  - chatGPTを利用して実装の助言やソースコードの解説をしてもらうことでより良い実装・学習になりそう。
  - 

```python
# 時間計算量：O(n)
# 空間計算量：O(n)
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []
        closeToOpen = { ")" : "(", "]" : "[", "}" : "{"}

        for c in s:
            if c in closeToOpen:
                if stack and stack[-1] == closeToOpen[c]:
                    stack.pop()
                else:
                    return False
            else:
                stack.append(c)
        return True if not stack else False
```

# Step3
かかった時間： 5min

上記を書き直して実装。

```python
# 時間計算量：O(n)
# 空間計算量：O(n)
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []
        closeToOpen = { ")" : "(", "]" : "[", "}" : "{" }

        for c in s:
            if c in closeToOpen:
                if stack and stack[-1] == closeToOpen[c]:
                    stack.pop()
                else:
                    return False
            else:
                stack.append(c)
        return True if not stack else False
```

# Step4 
- レビューを受けて修正を行う

```python


```
