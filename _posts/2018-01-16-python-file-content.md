---
layout: post
title: Python文件和目录操作(os 模块)
category: 实用库
tags:
  - python
---

目前在写代码的时候发现自己对代码的各类操作非常陌生,不写一写实在记不住。于是开启了Python学习笔记系列，主要用于记录自己学习python中各类知识的总结。

本篇是文件和目录操作，os模块。

# 目录操作

### 1、取得当前目录--os.getcwd()
```
import os
s = os.getcwd()
print(s)
```
此时会显示当前运行脚本所在的文件夹的位置

### 2、判断一个路径中是否有需要的文件--os.path.isfile("path")
```
import os
Path1 = "test.txt"
s1 = os.path.isfile()
print(s1)
Path2 = "C:\\Users\\hello-world.txt"
s2 = os.path.isfile()
print(s2)
```
s1是检测当前目录下是否存在名为test.txt的文件，s2则是检测具体路径Path2下是否存在hello-world.txt的文件

### 3、判断一个路径是否存在--os.path.isdir("path")
```
import os
print(os.path.isdir("C:\\")) # 输出为True
print(os.path.isdir("M:\\")) # 输出为False
```
显然，一般用户会有C盘但不会有M盘，所以第一个输出True,第二个输出False

### 4、判断一个路径(目录或文件)是否存在--os.path.exists("path")
```
import os
print(os.path.exists("C:\\")) # 路径存在 True
print(os.path.exists("M:\\")) # 路径不存在 True
print(os.path.exists("C:\\test1.txt")) # 文件存在 True
print(os.path.exists("C:\\test2.txt")) # 文件不存在 False
```

### 5、创建子目录--os.makedirs("path")
```
import os
os.makedirs("D:\\users\\test")
```
这样我们就创建了一个"D:\\users\\test"的目录，具体表现为空文件夹，但也有可能失败，比如路径已存在，或者驱动器不存在，或者权限不够等

### 6、更改当前目录--os. chdir(''path'')
```
import os
os. chdir(''C:\\'')
```
相当于dos或者Linux下的cd命令，将当前目录更改为''C:\\''

### 7、将路径分解为路径名和文件名--os.path.split()
```
import os
path,file = os.path.split("C:\\dir1\\test.txt")
```
path为"C:\\dir1"，file为"test.txt"

### 8、分解文件的扩展名--os.path.splitext()
```
import os
fpath_name,ftext = os.path.splitext("C:\\dir1\\test.txt")
```
此时，fpath_name为"C:\\dir1\\test"，ftext为".txt"

### 9、取得当前目录--os.listdir("path")
```
import os
file_list = os.listdir("C:\\") # 将会包含所有文件及子目录，包括隐藏文件
```

### 10、删除子目录--os.rmdir("path")
```
import os
os.rmdir("C:\\father\\son") # 这里只删除son目录
os.rmdir("C:\\father") # 这里才删除father目录
```

# 文件操作

### 打开文件--open('file'[,'mode'])

| 模式 | 描述 |
| ---- | ---- |
| r | 以读的方式打开文件，可以读取文件信息，为默认选项 |
| w | 以写的方式打开文件，可向文件写入信息。如文件存在，则清空并重新写入 |
| a | 以追加模式打开文件（即一打开文件，文件指针自动移到文件末尾），如果文件不存在则创建 |
| r+ | 以读写方式打开文件，可对文件进行读和写操作。 |
| w+ | 消除文件内容，然后以读写方式打开文件。 |
| a+ | 以读写方式打开文件，并把文件指针移到文件尾 |
| b | 以二进制模式打开文件，而不是以文本模式。该模式只对Windows或Dos有效，类Unix的文件是用二进制模式进行操作的 |

### 其他常见操作

| 操作 | 描述|
| --- | ---|
| f.close() | 关闭文件，open之后一定要关闭，否则会占用系统的可打开文件句柄数 |
| f.write(string) | 把string字符串写入文件，write()不会在str后加上一个换行符 |
| f.writelines(list) | 把list中的字符串一行一行地写入文件，是连续写入文件，没有换行 |
| f.name() | 获取文件名称 |
| f.next() | 返回下一行，并将文件操作标记位移到下一行。把一个file用于for … in file这样的语句时，就是调用next()函数来实现遍历的 |
| f.fileno() | 获得文件描述符，是一个数字。返回一个长整型的”文件标签“ |
| f.flush() | 刷新输出缓存，把缓冲区的内容写入硬盘 |
| f.isatty() | 如果文件是一个终端设备文件（Linux系统中），则返回True，否则返回False |
| f.read([size]) | 读出文件，size为读取的长度，以byte为单位 |
| f.readline([size]) | 读出一行信息，若定义了size，则读出 一行的一部分 |
| f.readlines([size]) | 读出所有行，也就是读出整个文件的信息。(把文件每一行作为一个list的一个成员，并返回这个list。其实它的内部是通过循环调用readline()来实现的。如果提供size参数，size是表示读取内容的总长，也就是说可能只读到文件的一部分) |
| f.seek(offest[,where]) | 把文件指针移动到相对于where的offset位置。where为0表示文件开始处，这是默认值 ；1表示当前位置；2表示文件结尾。(注意：如果文件以a或a+的模式打开，每次进行写操作时，文件操作标记会自动返回到文件末尾) |
| f.tell() | 获得文件指针位置，标记当前位置，以文件开头为原点 |
| f.truncate([size]) | 把文件裁成规定的大小，默认的是裁到当前文件操作标记的位置。如果size比文件的大小还要大，依据系统的不同可能是不改变文件，也可能是用0把文件补到相应的大小，也可能是以一些随机的内容加上去 |




