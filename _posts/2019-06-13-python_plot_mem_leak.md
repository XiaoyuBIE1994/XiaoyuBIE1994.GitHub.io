---
layout: post
title: Python循环画图时内存泄露的问题
category: 代码踩坑
tags: 
  - python
---



前几天干活的时候，使用了 `matplotlib.pyplot` 批量生成图片并保存，结果发生了内存泄露，内存使用量不同的增加到最后电脑卡死。最后发现是生成的图片在内存中不断堆积导致，需要改进一下两个方面：

- 当我们不需要展示图片时，需要使用`matplotlib` 的非交互模式，比如 `agg`
- 每一步生成图片并保存后需要进行内存清理

测试的代码如下：

```python
import matplotlib as mpl
mpl.use('Agg')
print(mpl.get_backend())
import matplotlib.pyplot as plt
import numpy as np
import psutil
import gc
import os
import shutil

process = psutil.Process(os.getpid())
test_dir = "Test"
os.mkdir(test_dir)
mem = open('memory_pyplot_00.txt', 'w')
mem.write("Mode: default, show: no, mem_clean: yes\n")

for i in range(500):    
    if i % 10 == 0:
        mem_str = "Memory used: {} Mb\n".format(process.memory_info().rss // 1e6)
        print(mem_str)
        mem.write(mem_str)   
    fig = plt.figure()
    ax = fig.add_subplot(1, 1, 1)
    ax.scatter(np.random.random(10), np.random.random(10))
#    plt.show()
    fig.savefig('Test/test.png')
    fig.clf()
    plt.close(fig)
    gc.collect()  

mem.close()
shutil.rmtree(test_dir)
```



变量为是否改变交互模式，是否进行内存清理，是否每一步进行进行展示 (`plt.show()`，非交互模式下不能进行展示)，结果如下

```txt
Mode: default, show: no, mem_clean: no
Memory used: 102.0 Mb
Memory used: 118.0 Mb
Memory used: 130.0 Mb
Memory used: 142.0 Mb
Memory used: 153.0 Mb
Memory used: 165.0 Mb

Mode: default, show: no, mem_clean: yes
Memory used: 103.0 Mb
Memory used: 113.0 Mb
Memory used: 119.0 Mb
Memory used: 124.0 Mb
Memory used: 130.0 Mb
Memory used: 136.0 Mb

Mode: default, show: yes, mem_clean: no
Memory used: 103.0 Mb
Memory used: 119.0 Mb
Memory used: 121.0 Mb
Memory used: 122.0 Mb
Memory used: 122.0 Mb
Memory used: 122.0 Mb

Mode: default, show: yes, mem_clean: yes
Memory used: 103.0 Mb
Memory used: 109.0 Mb
Memory used: 109.0 Mb
Memory used: 109.0 Mb
Memory used: 109.0 Mb
Memory used: 109.0 Mb

Mode: Agg, show: no, mem_clean: no
Memory used: 103.0 Mb
Memory used: 118.0 Mb
Memory used: 130.0 Mb
Memory used: 142.0 Mb
Memory used: 153.0 Mb
Memory used: 165.0 Mb

Mode: Agg, show: no, mem_clean: yes
Memory used: 105.0 Mb
Memory used: 110.0 Mb
Memory used: 110.0 Mb
Memory used: 110.0 Mb
Memory used: 110.0 Mb
Memory used: 110.0 Mb
```



可以发现，在默认模式下，每一步进行 `plt.show()`可以避免内存泄露，是否对每一个 `fig`进行清理并不是很重要。而如果不想要在终端画出每一张图，就需要改成非交互模式（需要在 `import matplotlib.pyplot as plt`之前进行改变）并且每一步进行内存清理，`gc.collect() `是 Python 的垃圾回收，是否加上这一步对实验结果影响不大（测试代码中的500张图和实际实验中将近2W张不影响，至于图片数量继续增加的情况下是否有影响暂时不清楚）