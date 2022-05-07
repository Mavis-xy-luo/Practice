# Sort
## 细说.sort()中的key
参考：https://docs.python.org/zh-cn/3/howto/sorting.html

**list.sort( key = None, reverse = False)**

key -- 用来进行比较的元素，只有一个参数（具体函数参数取自可迭代对象中，指定可迭代对象中的一个元素来进行排序）

常规：默认排序顺序  
默认按0位排序，再依次往后，按1位排序
```python
li = [[5, 6], [1, 8], [3, 2]]
li.sort()

>> [[1, 8], [3, 2], [5, 6]]
```

根据指定位置排序
```python
li.sort(key = lambda x: x[1])
# x这个字母可以随意切换： li.sort(key = lambda li: li[1])

>> [[3, 2], [5, 6], [1, 8]]
```

以上lambda函数形式可以写成如下自定函数形式  
1. 使用对象的一些索引作为key对复杂对象进行排序
```python
def fun(li):
    return li[1]

#将函数fun传递给参数key
li.sort(key = fun)

>> [[3, 2], [5, 6], [1, 8]]
```

2. 也可以用于具有命名属性的对象
```python
class Student(object):
    def __init__(self, name, grade, age):
        self.name = name
        self.grad = grad
        self.age = age

    def __repr__(self):
        return repr((self.name, slef.grad, slef.age))
    

student_objects = [
    Student('John', 'A', 15),
    Student('Jane', 'B', 12),
    Student('Dave', 'B', 10)
]


sorted(student_objects, key=lambda student: student.age)   # sort by age

>> [('Dave', 'B', 10), ('Jane', 'B', 12), ('John', 'A', 15)]
```
<br>

ex. 根据字符串中不同字母的数量对一个字符串集合进行排序  
strings = ['foo', 'card', 'bar', 'aaaa', 'abab' ]
```python
strings.sort(key = lambda: x: len(set(list(x))) )

>> [‘aaaa’, ‘foo’, ‘abab’, ‘bar’, ‘card’]
```
