# enumerate()

enumerate 对象产生的对包含一个计数（从开始，默认为零）和一个由 iterable 参数产生的值。

enumerate is useful for obtaining an indexed list:
(0, seq[0]), (1, seq[1]), (2, seq[2]), ...

```python
for idx, line in enumerate(lines):
    pass
```