# Code problems collection

#### not和or/and的优先级问题
not > and > or

```python
(not A or B) and C
```

1. not A or not B
2. (not A) or B

not的优先级>or的优先级，故2对
