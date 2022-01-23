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
Flse: 所有空字符串，包括0
True: 所有非空字符串，非0数字
<br>

**and**  
返回第一个F的值；如果都是T，返回右边表达式的值
<br>

**or**  
返回第一个T的值；如果都是F，返回右边表达式的值

[参考资料](https://blog.csdn.net/weixin_39875760/article/details/109931256?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-0.pc_relevant_default&spm=1001.2101.3001.4242.1&utm_relevant_index=3)

```python
print( 2 and 0 and 5)  
>> 0
print(2 and 2 and 5)
>> 5
print(None and 0)
>> 0

print(3 or 0 or None)  
>> 3
print(0 or 5 or None)
>> 5
print(None or 0)
>> None
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

Red-Black Tree
AVL Tree
Splay Tree


### Tail Recursion
A tail recursion is a recursive function where the function calls itself at the end("tail") of the function in which no computation is done after the return of the recursive call.  

**Tail Recursion can always be translated to iterative calls.**


