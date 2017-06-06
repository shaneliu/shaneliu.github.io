---
layout:     post
title:      "Python 清空文件内容"
subtitle:   " \"How to delete only the content of file in python\""
date:       2017-05-24 12:00:00
author:     "iamshane"
header-img: "img/python-logo.jpg"
tags:
    - Python
    - 代码
    - 文件操作
    - 删除
--- 


### 清空一个打开的文件

```python
def delete_content( pfile ):
    pfile.seek(0)
    pfile.truncate()
```
---

### 清空一个打开的文件，并且文件句柄是已知的

```python
def delete_content(fd):
    os.ftruncate(fd, 0)
    os.lseek(fd, 0, os.SEEK_SET)
```

---

### 清空一个关闭的文件（文件名已知）

##### 这个方法简单，并且可行

```python
def delete_content(fName):
    try:
        with open(fName, "w") as data:
            pass
    except IOError as e:
        print 'IO error' + str(e)
```

##### 也可以使用一条命令，直接打开文件写并覆写就会清空（注意，不能使用增加参数'a'）

```python
open(filename, 'w').close()
```

---

### 参考资料

- [How to delete only the content of file in python](https://stackoverflow.com/questions/17126037/how-to-delete-only-the-content-of-file-in-python)
- [python清空文件内容· Cloud Atlas-huataihuang-GitBook](https://huataihuang.gitbooks.io/cloud-atlas/content/develop/python/startup/delete_content_of_file.html)




