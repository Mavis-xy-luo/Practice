# Dict & Set

## Create new dict

``` python
my_dict = {}
grades = {'Ana' : 'A', 'Bob' : 'C'}
```

## look-up

``` python
grades['Ana']   # get 'A'
grades['David']   # gives a KeyError
```
Avoid KeyError: ***dictionary.get(key, default_val)***

```python
grades.get('Ana', 'N')   # get 'A'
grades.get('David', 'N')   # get 'N'
```

## Add
``` python
grades['Cythia'] = 'B+'
```

## Update
The same syntax as "Add"
``` python
grades['Ana'] = 'A+'
```

## Delete
``` pyhton
# method 1
del grades['Bob']

# method 2
grades.pop('Bob')
```

## Other uses
### get keys and values
**Get all keys as a list**
``` python
list(grades.keys())   
```
**Get all values as a list**
``` python
list(grades.values())
```

**Get all items**
``` python
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



------ 
## Create new set
``` python
s = set()   # 区分tuple的创建，t = ()
s = {'a', 'b', 'c'}
```

## Add
``` python
s.add('d')
s.update({'e', 'f'})
```

## Delete
``` python
s.remove('a')
s.discard('i')

s.clear()   # clear all elements from set
```
 
## Other uses
### Union two sets
``` python
x.union(y)   # 会去除重复，因为set
```

### Difference between two sets
``` python
x.difference(y)   # x中有，y没有的
y.difference(x)   # y中有，x没有的
```

### intersection
``` python
s.intersection(y)   # 2者都有的
```

### Operators for sets
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


