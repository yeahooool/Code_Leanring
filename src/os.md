# import os

1. `os.walk()`: yields a 3-tuple:(root, dirs, files) // dirpath, dirnames, filenames
2. `os.path.abspath(path)`: Return an absolute path.
3. `os.path.exists(workDir)`: Test whether a path exists. Returns False for broken symbolic links
4. `os.path.join(a, *p)`: Join two or more pathname components, inserting '/' as needed. If any component is an absolute path, all previous path components will be discarded. An empty last part will result in a path that ends with a separator.
5. `os.system(command)`: system 函数可以将字符串转化成命令在服务器上运行---如`command = "gen_dR.x | tee ./output/out"`
6. `os.makedirs()`,`os.mkdir()`：前者创建多层目录，如果前面的目录不存在会自动创建；后者创建路径中的最后一级目录，如果之前的目录不存在并且也需要创建的话就会报错。
7. `os.path.split()` and `split(',')`: split()：拆分字符串。通过指定分隔符对字符串进行切片，并返回分割后的字符串列表（list）; os.path.split()：按照路径将文件名和路径分割开。
