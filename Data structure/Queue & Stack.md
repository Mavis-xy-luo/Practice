# Queue & Stack



## 遇到题目的注意点：
在构建环形Queue时： 

一、第一种设计思路：first指向真的first元素的位置，last指向真的last元素的位置（数据集的空间刚好等于其容量空间n=k)
注意：当数据集为空集时，从尾端push元素，last往前走一位，会出现last跑到了first前面的问题。（故空集时从后插入数据需要列如特殊考虑）

二、第二种设计思路：first指向真的first元素前面一个位置，last指向真的last元素后面一个位置（即数据集空间比其容量空间多一个位置n=k+1）

这两者思路在出现first/last - 1得到新的first/last位置时需要考虑为负数的情况：即-1；

—— 通过这种方式可以确保得到的位置会永远在范围内（first/last - 1 + len(items)) % len(items)  


**常见操作**
```python
from collections import deque

q = deque()
deque([iterable])

q.append()
q.appendleft()

q.extend()
q.extendleft()

q.pop()
q.popleft()

q.clear() # remove all values from queue

q.count(val) # return number of occurrences of value

q.remove(val) # remove and return first occurrence of value
q.reverse() # reverse in place

```
