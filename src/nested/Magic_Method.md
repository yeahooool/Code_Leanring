# 魔术方法（Magic Method)

1. `__getitem__`: Python中的一个魔术方法，用于实现对象的索引访问。当我们使用`[]`符号对一个对象进行索引操作时，实际上是在调用这个对象的`__getitem__`方法。
    
    `__getitem__`方法接收一个参数`key`，表示索引值，然后根据索引值返回相应的值。如果`key`是整数，则表示索引访问；如果`key`是切片对象，则表示切片访问。如果`key`不是合法的索引值，则抛出`IndexError`异常。
    
    下面是一个示例，演示如何定义`__getitem__`方法来实现对象的索引访问：
    ```python
    class MyList:
    def __init__(self, data):
        self.data = data

    def __getitem__(self, key):
        if isinstance(key, int):
            if key < 0 or key >= len(self.data):
                raise IndexError('list index out of range')
            return self.data[key]
        elif isinstance(key, slice):
            start, stop, step = key.start, key.stop, key.step
            start = start or 0
            stop = stop or len(self.data)
            step = step or 1
            return [self.data[i] for i in range(start, stop, step)]
        else:
            raise TypeError('indices must be integers or slices')
    ```
    在上面的代码中，我们定义了一个`MyList`类，它包含一个列表数据`data`。然后，我们在类中定义了`__getitem_`_方法，它接收一个参数`key`，表示索引值。如果`key`是整数，我们检查索引值是否合法，然后返回相应的元素。如果`key`是切片对象，我们解析切片对象，然后返回切片所表示的元素列表。如果`key`既不是整数也不是切片对象，则抛出`TypeError`异常。

    使用上述代码，我们可以像使用普通列表一样使用`MyList`对象进行索引访问和切片访问：
    ```python
    mylist = MyList([1, 2, 3, 4, 5])
    print(mylist[0])       # 输出1
    print(mylist[-1])      # 输出5
    print(mylist[1:3])     # 输出[2, 3]
    print(mylist[::2])     # 输出[1, 3, 5]
    ```

2. `__len__`: Python中的一个魔术方法，用于实现对象的长度计算。当我们使用`len()`函数对一个对象进行长度计算时，实际上是在调用这个对象的`__len__`方法。

    `__len__`方法不接收任何参数，它应该返回一个整数，表示对象的长度。如果对象没有长度，则应该抛出`TypeError`异常。
    
    下面是一个示例，演示如何定义`__len__`方法来实现对象的长度计算：
    ```python
    class MyList:
        def __init__(self, data):
            self.data = data
    
        def __len__(self):
            return len(self.data)
    ```
    在上面的代码中，我们定义了一个`MyList`类，它包含一个列表数据`data`。然后，我们在类中定义了`__len__`方法，它返回列表数据的长度。

    使用上述代码，我们可以像使用普通列表一样使用`MyList`对象进行长度计算：
    ```python
    mylist = MyList([1, 2, 3, 4, 5])
    print(len(mylist))     # 输出5
    ```
    注意，Python中许多内置类型都实现了`__len__`方法，如列表、元组、字符串等。因此，当我们使用`len()`函数计算这些对象的长度时，也是调用它们的`__len__`方法。