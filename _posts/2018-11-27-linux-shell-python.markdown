---
layout: post
title:  "shell调用python"
date:   2018-11-27 16:15:45
categories: linux shell
---
### 简单地用shell调用python

- 两个文件 

test.sh
```shell
python /.../test.py
```

test.py
```python
print('test')
```

### 用shell传参数调用python
- 两个文件 

test.sh
```shell
a=1
b=2
python /.../test.py $a $b
```

test.py
```python
import sys
def main(x,y):
    print ('x:',x)
    print ('y:',y)

main(sys.argv[1],sys.argv[2])
```

|文件|test.sh|test.py|
|:--:|:--:|:--:|
|变量1|a|sys.argv[1]|
|变量2|b|sys.argv[2]|
