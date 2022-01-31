# Dict & Set
<br>

## Dict
key是immutable的，所以key必须是immutable(hashable)的数据类型，所以list不行，tuple可以作为key。  
<br>
**Create new dict**
``` python
my_dict = dict()
my_dict = {}
grades = {'Ana' : 'A', 'Bob' : 'C'}
```

**look-up**
``` python
grades['Ana']   # get 'A'
grades['David']   # gives a KeyError
```
Avoid KeyError: ***dictionary.get(key, default_val)***

```python
grades.get('Ana', 'N')   # get 'A'
grades.get('David', 'N')   # get 'N'
```

**Add**
``` python
grades['Cythia'] = 'B+'
```
**Update**
The same syntax as "Add"
``` python
grades['Ana'] = 'A+'
```

**Delete**
``` pyhton
# method 1
del grades['Bob']

# method 2
grades.pop('Bob')
```

**Other uses**  
**get keys and values**
``` python
# Get all keys as a list
list(grades.keys())   

# Get all values as a list
list(grades.values())

# Get all items
grades.items()   # returns dict_items([('Ana', 'A'), ('Bob', 'C')])

```

**Use Cases**  
Most common word in a frequency dictionary
``` python
def most_common_words(freqs):
	best = max(freqs.values())
	words = []
	for word, count in freqs.items():
		if count == best:
			words.append(word)
	return (words, best)
```
<br>

------ 

<br>

## collections.defaultdict(list/int/str)
create a dict with list/int/str类型的value
```python
import collections
de_dict = collections.defaultdict(list)

print(type(de_dict)
>> <class 'collections.defaultdict'>

```
<br>

------ 
<br>

## Set
unordered collection of unique elements  
<br>
**Create new set**
``` python
s = set()   # 区分tuple的创建，t = ()
s = {'a', 'b', 'c'}
```

**Add**
``` python
s.add('d')
s.update({'e', 'f'})
```

**Delete**
``` python
s.remove('a')
s.discard('i')

s.clear()   # clear all elements from set
```
 
**Other uses**  
**Union two sets**
``` python
x.union(y)   # 会去除重复，因为set
```

**Difference between two sets**
``` python
x.difference(y)   # x中有，y没有的
y.difference(x)   # y中有，x没有的
```

**intersection**
``` python
s.intersection(y)   # 2者都有的
```

**Operators for sets**
``` python
if key in s
if key not in s
s1 == s2
s1 != s2
s1 <= s2   # s1 is subset of s2
s1 < s2   # s1 is proper subset of s2
s1 > s2   # s1 is proper superset of s2
s1 | s2   # the union of s1 and s2
s1 & s2   # the intersection of s1 and s2
s1 - s2   # set of elements in s1 but not in s2
s1^s2   # the set of elements in precisely one of s1 or s2 留下只有s1有或者只有s2有的元素
```


