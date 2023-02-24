# import pathlib

1. `pathlib.Path(PurePath)`: PurePath subclass that can make system calls.

    ```python
    p = Path('D:/python/1.py')
    >>> D:\python\1.py
    
    #可以这么使用,相当于os.path.join()
    p1 = Path('D:/python')
    p2 = p1/'123'
    >>> D:\python\123
    ```

    
    > `Path(__file__)`中`__file__`的作用是在执行python文件时，把当前目录添加到sys.path中，配合[sys.path](sys.md)使用:
    `codepath = str(pathlib.Path(__file__).parent.resolve())`
   ` sys.path.append(codepath)`
    

2. `Path.cwd()`: 获取当前路径

3. `Path.parent()`: 以字符串的形式返回作为参数传递的路径的父目录。

    ```python
    from pathlib import Path

    path1 = Path(r"C:\folder\subfolder\myfile.txt")
    path2 = Path(r"C:\Myfile.txt")
    print(path1.parent)
    print(path2.parent)

    >>> 
    C:\folder\subfolder
    C:\
    ```

4. `Path.resolve()`: 将路径或路径片段的序列解析为绝对路径
   * 对于给定的路径片段，是**从右向左**拼接处理，直至构造出绝对路径;
   * 如果在处理完所有给定的 path 片段之后还未生成绝对路径，则需要加上当前工作目录。

    ```python
    var path = require("path")     //引入node的path模块
    
    path.resolve('/foo/bar', './baz')   // returns '/foo/bar/baz'
    path.resolve('/foo/bar', 'baz')   // returns '/foo/bar/baz'
    path.resolve('/foo/bar', '/baz')   // returns '/baz'
    path.resolve('/foo/bar', '../baz')   // returns '/foo/baz'
    path.resolve('home','/foo/bar', '../baz')   // returns '/foo/baz'
    path.resolve('home','./foo/bar', '../baz')   // returns '当前工作目录/home/foo/baz'
    path.resolve('home','foo/bar', '../baz')   // returns '当前工作目录/home/foo/baz'
    ```
    相当于：
    ```python
    path.resolve('/foo/bar', '../baz')  

    >>> 
    cd /foo/bar
    cd ..
    cd baz
    ```