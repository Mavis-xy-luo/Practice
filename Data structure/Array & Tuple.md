# Array

**增**
```python
lst = []
lst.append(val)   # add an element to the end of list
lst.extend(lst2)   # add another list to the end of list
```

**删**
```python

lst.remove(val)   # remove first occurence of the val
del(lst[idx])   # delete element at a specific index
lst.pop()   # remove the last element

```

**查**
```python

lst[idx]
lst[0]
lst[-1]

```

**改**
```python

lst[idx] = val

```

**遍历 iterable**
```python

# iterate on list
for val in lst:

```

**Slicing**
```python

lst[start:end:step]   # [start, end) end cannot be arrive, 走step步取1次

```
**Packing & Unpacking**  
> list 的packing很有意思，地址传递，所以改packing前的容器内的值，packing后的list 以及 之后unpacking后variable的所指之值也会被改变
```python

name = "Cythia"
times = [1,2,3]
lst = [name, times]

name_1, times_1 = lst
print(lst)   # before alter
print(name_1)
print(times_1)

times[2] = 5
print(lst)   # after alter
print(name_1)
print(times_1)

>> ['Cythia', [1, 2, 3]]
   Cythia
   [1, 2, 3]
>> ['Cythia', [1, 2, 5]]
   Cythia
   [1, 2, 5]
   
```



**Otehr function**
```python
# get length of a list
len(lst)

# sort
new_lst = soreted(lst)   # not inplace, do not mutate lst, returns sorted lst
lst.sort()   # in place sort, mutate lst

# reverse
lst.reverse()   # in place reverse lst

# to string
"".join(lst)   # 用引号内的元素把lst中每个元素连接起来
```
<br>




<br>

# Tuple
- Immutable
- ordered
- mix element types  

**Create**
```python

tup = ()
tup = ('a', 'b', 'c')

```
因为是immutable，所以没有增、删、改
> 虽然tuple不可修改，但里面所存之容器内的值却可以修改，如list

```python

tu = ([1, 2, 3], "a", "b")
tu[0][0] = 5   # 如果 tu[1] = "c" 会报错，因为这是reassignment，而前者是modify
print(tu)

>> ([5, 2, 3], 'a', 'b')
```

**Packing & Unpacking**
```python
# packing
name = "abc"
author = "Ana"
genre = "Math"

tup = (name, genre, author)
print(tup)

>> ('abc', 'Math', 'Ana')


# unpacking
tup = ("ABC", "Ana", "CS")

bookName, author, genre = tup
(bookName, author, genre) = tup
print(bookName)
print(author)
print(genre)

>> ABC
>> Ana
>> CS

```

**iterable**
``` python
for immu_val in tup:
```

