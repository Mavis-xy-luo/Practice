# Code problems collection

#### not和or/and的优先级问题
not > and > or

```python
(not A or B) and C
```

1. not A or not B
2. (not A) or B

not的优先级>or的优先级，故2对


#### or 和 and返值问题  

```python
print( 3 or 1)  
>> 3  
print( 3 and 1)  
>> 1
```

--------
#### dict

1. dictA遍历得到的是什么？
   for i in dictA 遍历的是key
   
2. dict的妙用
   不需要判断这个元素i在不在dict里，直接计入dict计数
   dictA.get(i, 0) + 1
   
#### list
list.append(A) ---- 把A作为一个元素append进来
list.extend(A) ---- 把A里的元素加进来

```python
lst1 = [0, 1, 2]
lst2 = [3]
lst3 = [4, 5]

lst1.append(lst2 * 2) / lst1.append([3] * 2)   # [0, 1, 2, [3], [3]]
lst1.extend(lst2 * 2) / lst1.extend([3] * 2)   # [0, 1, 2, 3, 3]
lst1 += lst2 * 2 / lst1 += [3] * 2   # [0, 1, 2, 3, 3]

lst1.append(lst3 * 2)  # [0, 1, 2, [4, 5], [4, 5]]
lst1.extend(lst3 * 2)   # [0, 1, 2, 4, 5, 4, 5]
lst1 += lst3 * 2  # [0, 1, 2, 4, 5, 4, 5]

```

-----------

list comprehension
x for x in a if x in b (返回的是list)
set comprehension
set()函数的时间复杂度
set comprehension的时间
set comprehension



