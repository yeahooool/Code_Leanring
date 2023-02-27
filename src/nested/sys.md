# import sys

<<<<<<< HEAD
`sys.path`指定模块搜索路径的列表。默认情况下，python 导入文件或者模块，会在`sys.path`里找模块的路径。如果在当前搜索路径列表`sys.path`中找不到该模块的话，就会报错。

---

最常用的用法就是向`sys.path`中添加搜索路径

```python
import sys
sys.path.append(path)  # path 代表的是一个路径
```

---

使用示例:

- 查看当前搜索路径

```python
In [2]: import sys

In [3]: sys.path
Out[3]: 
['/data/home/hfhuang/software/anaconda3/envs/p100/bin',
 '',
 '/opt/rh/devtoolset-8/root/usr/lib64/python2.7/site-packages',
 '/opt/rh/devtoolset-8/root/usr/lib/python2.7/site-packages',
 '/data/home/hfhuang/software/PWmatMLFF/src',
 '/data/home/hfhuang/software',
 '/data/home/hfhuang/software/anaconda3/envs/p100/lib/python38.zip',
 '/data/home/hfhuang/software/anaconda3/envs/p100/lib/python3.8',
 '/data/home/hfhuang/software/anaconda3/envs/p100/lib/python3.8/lib-dynload',
 '/data/home/hfhuang/.local/lib/python3.8/site-packages',
 '/data/home/hfhuang/software/anaconda3/envs/p100/lib/python3.8/site-packages',
 '/data/home/hfhuang/software/anaconda3/envs/p100/lib/python3.8/site-packages/op-0.0.0-py3.8-linux-x86_64.egg']
```

- 意思是导入python模块时,需要从这些路径中寻找

- 添加新的搜索路径
  - 假设我要导入一个模块`md100`,路径为`/data/home/hfhuang/software/PWmatMLFF/src/pre_data/`,直接`import md100`,显示报错:
```python
In [4]: import md100
---------------------------------------------------------------------------
ModuleNotFoundError                       Traceback (most recent call last)
Cell In[4], line 1
----> 1 import md100

ModuleNotFoundError: No module named 'md100'
```
  - 添加路径后重新import:

```python
In [5]: sys.path.append('/data/home/hfhuang/software/PWmatMLFF/src/pre_data/')

In [6]: import md100

In [7]: sys.path
Out[7]: 
['/data/home/hfhuang/software/anaconda3/envs/p100/bin',
 '',
 '/opt/rh/devtoolset-8/root/usr/lib64/python2.7/site-packages',
 '/opt/rh/devtoolset-8/root/usr/lib/python2.7/site-packages',
 '/data/home/hfhuang/software/PWmatMLFF/src',
 '/data/home/hfhuang/software',
 '/data/home/hfhuang/software/anaconda3/envs/p100/lib/python38.zip',
 '/data/home/hfhuang/software/anaconda3/envs/p100/lib/python3.8',
 '/data/home/hfhuang/software/anaconda3/envs/p100/lib/python3.8/lib-dynload',
 '/data/home/hfhuang/.local/lib/python3.8/site-packages',
 '/data/home/hfhuang/software/anaconda3/envs/p100/lib/python3.8/site-packages',
 '/data/home/hfhuang/software/anaconda3/envs/p100/lib/python3.8/site-packages/op-0.0.0-py3.8-linux-x86_64.egg',
 '/data/home/hfhuang/software/PWmatMLFF/src/pre_data/']
```
=======
1. `sys.path`: 指定模块搜索路径的列表。默认情况下，python 导入文件或者模块，会在`sys.path`里找模块的路径。如果在当前搜索路径列表`sys.path`中找不到该模块的话，就会报错。

   最常用的用法就是向`sys.path`中添加搜索路径

   ```python
   import sys
   sys.path.append(path)  # path 代表的是一个路径
   ```

   <details>
   <summary>使用示例:</summary>
     
   - 查看当前搜索路径
     
   ```python
   In [2]: import sys

   In [3]: sys.path
   Out[3]:
   ['/data/home/hfhuang/software/anaconda3/envs/p100/bin',
   '',
   '/opt/rh/devtoolset-8/root/usr/lib64/python2.7/site-packages',
   '/opt/rh/devtoolset-8/root/usr/lib/python2.7/site-packages',
   '/data/home/hfhuang/software/PWmatMLFF/src',
   '/data/home/hfhuang/software',
   '/data/home/hfhuang/software/anaconda3/envs/p100/lib/python38.zip',
   '/data/home/hfhuang/software/anaconda3/envs/p100/lib/python3.8',
   '/data/home/hfhuang/software/anaconda3/envs/p100/lib/python3.8/lib-dynload',
   '/data/home/hfhuang/.local/lib/python3.8/site-packages',
   '/data/home/hfhuang/software/anaconda3/envs/p100/lib/python3.8/site-packages',
   '/data/home/hfhuang/software/anaconda3/envs/p100/lib/python3.8/site-packages/op-0.0.0-py3.8-linux-x86_64.egg']

   ````

   - 意思是导入python模块时,需要从这些路径中寻找

   - 添加新的搜索路径
     - 假设我要导入一个模块`md100`,路径为`/data/home/hfhuang/software/PWmatMLFF/src/pre_data/`,直接`import md100`,显示报错:
   ```python
   In [4]: import md100
   ---------------------------------------------------------------------------
   ModuleNotFoundError                       Traceback (most recent call last)
   Cell In[4], line 1
   ----> 1 import md100

   ModuleNotFoundError: No module named 'md100'
   ````

   - 添加路径后重新 import:

   ```python
   In [5]: sys.path.append('/data/home/hfhuang/software/PWmatMLFF/src/pre_data/')

   In [6]: import md100

   In [7]: sys.path
   Out[7]:
   ['/data/home/hfhuang/software/anaconda3/envs/p100/bin',
     '',
     '/opt/rh/devtoolset-8/root/usr/lib64/python2.7/site-packages',
     '/opt/rh/devtoolset-8/root/usr/lib/python2.7/site-packages',
     '/data/home/hfhuang/software/PWmatMLFF/src',
     '/data/home/hfhuang/software',
     '/data/home/hfhuang/software/anaconda3/envs/p100/lib/python38.zip',
     '/data/home/hfhuang/software/anaconda3/envs/p100/lib/python3.8',
     '/data/home/hfhuang/software/anaconda3/envs/p100/lib/python3.8/lib-dynload',
     '/data/home/hfhuang/.local/lib/python3.8/site-packages',
     '/data/home/hfhuang/software/anaconda3/envs/p100/lib/python3.8/site-packages',
     '/data/home/hfhuang/software/anaconda3/envs/p100/lib/python3.8/site-packages/op-0.0.0-py3.8-linux-x86_64.egg',
     '/data/home/hfhuang/software/PWmatMLFF/src/pre_data/']
   ```

   </details>

2. `sys.argv`: 一个从程序外部获取参数的桥梁。因为我们从外部取得的参数可以是多个，所以获得的是一个列表（list)，也就是说 sys.argv 其实可以看作是一个列表，所以才能用[]提取其中的元素。其第一个元素是程序本身，随后才依次是外部给予的参数。

   <details>
   <summary>使用示例:</summary>

   * 假设存在文件*test.py*, 执行代码时：

   ```python
   import sys
   a=sys.argv
   b=len(sys.argv)
   print(a)
   print(b)

   >>> ['test.py',]
       1
   ```
   *  再次运行代码python test.py coding:

   ```python
   >>> ['test.py', 'coding']
       2
   ```
   </details>

3. 
>>>>>>> 3a98cd2 (update)
