# 文件和异常

## 从文件中读取数据
* 要使用文件，首先得打开文件
* 函数`open(file_name)`接受一个参数，是`文件名`，返回的是一个表示`文件的对象`
* `with`关键字能够在不需要访问文件后将其关闭，这就不需要自己手动关闭这些文件
* `read()`方法返回的是一个长长的字符串
``` python
with open('pi.txt') as file_obj:
    content = file_obj.read()
    print(content.rstrip())
```

文件路径
* 前面的代码中，需要满足文本文件和`.py`源程序文件在同一个目录下面
* 也可以使用`相对路径`
    ``` python
    with open('sub_folder/pi.txt') as file_obj
    ```
* 也可以使用`完整路径名`
    ``` python
    with open('C:\Users\ryebooty\Desktop\Python-Learning-Notes\pi.txt')
    ```
    注意：在 Linux 系统中，使用的是斜杠`/`，但是在 Windows 系统中使用的是反斜杠`\`


逐行读取
``` python
with open('pi.txt') as file_obj:
    for line in file_obj:
        print(line)
```
* 由于读取到的每一行末尾都包含一个看不见的`\n`，因此每行读取之后将包含两个`\n`一个来自文件一个来自 print 函数。
* 使用`rstrip()`函数去掉这些`\n`
``` python
with open('pi.txt') as file_obj:
    for line in file_obj:
        print(line.rstrip())
```

创建一个包含文件所有行的列表
* 列表中的每一项都是文件中的一行
``` python
with open('pi.txt') as file_obj:
    lines = file_obj.readlines()  # 返回的是一个列表
```
* **读取文本文件时，python 将所有的内容全部解读为字符，可以使用`int`或者`float()`将内容转换为整数或者浮点数。**

判断一个字符串是否包含在另一个字符串中
* 直接使用关键字 `in`
``` python
longstr = 'iamtanjuntao and i come from hefei university of technology'
shortstr = 'juntao'
print(shortstr in longstr)   # 结果是 True
```


## 写入文件

使用 `open()` 函数打开文件时，提供参数
* `r` 读取模式
* `w` 写入模式
* `r+` 读取+写入模式
* `a` 附加模式

如果没有指定参数，那么 python 默认是以**只读**的方式打开文件。
* 如果指定的文件不存在，那么 python 将自动创建它；如果文件已存在，那么在使用`w`写入时，文件中原先的内容将被清空。


写入多行
* `write()` 函数不会在文本末尾添加换行符，需要手动添加`\n`，这样才能够实现`多行写入`。
    ``` python
    file_obj.write('hello\n')
    file_obj.write('world\n')
    ```

附加到文件
* 如果不想新写入的内容覆盖掉文件中原有的内容的话，那么可以使用`附加模式`打开文件，这样使用`write()`写入内容时，将会附加在原文件尾部，而不会覆盖掉原有内容
``` python
with open('file_path', 'a') as file_obj:
    file_obj.write('hello\n')
    file_obj.write('world\n')
```

## 异常

* 使用`try-except-else`结构实现异常管理
* `try` 可能出现异常的代码
* `except` 出现异常后，如何处理异常的代码
* `else` 没有出现异常，正确运行时的代码

例子
``` python
while True:
    first = raw_input("input the first number")
    if first == 'q':
        break
    second = raw_input("input the second number")
    if second == 'q':
        break

    try:
        ans = int(first) / int(second)
    except ZeroDivisionError:
        print("can't divided by zero")
    else:
        print(str(ans))
```


如何分词？--使用函数`split()`
``` python
sentence = "hi i am tanjuntao coming from hefei university of technology"
words = sentenct.split()   # 返回一个包含所有单词的列表
for word in words
    print(word)
```

出现异常时一声不吭
* 就是在`except`代码块中什么都不做，可以使用关键字`pass`
``` python
try:
    do something...
except:
    pass
else:
    do something...
```

## 存储数据

* `json:javascript object notation`是一种保存数据的格式
* 可以将 python 中的数据（列表、字典）等存储到 json 文件中
* 使用 `pump(data_structure, file_object)` 存储数据
* 使用 `load(file_object)` 来读取数据

演示：
``` python
import json
nums = list(range(31))
with open('file_path') as file_obj:
    json.pump(nums, file_obj)  # 将list写入json文件中

nums2 = json.load(file_obj)    # 从json文件中读取数据
print(nums2)
```


**重构**
* 简单说:就是代码本来是可以正确运行的，但是为了代码更加清晰、更加容易理解，需要将代码划分为一系列完成具体任务的函数。

下面的代码演示了一个过程：在没有用户时，创建一个用户并且写入到文件中如果已经存在用户，那么直接从文件中读取用户名。
``` python
import json
file_path = 'username1.json'


def greeter():
    try:
        with open(file_path) as file_obj:
            user_name = json.load(file_obj)

    except IOError:
        print("no such user, we will create a new user")
        user_name = raw_input('input your name: ')
        print("welcome " + user_name + "you are new to this website")
        # 使用写入模式，这样没有文件时也能够创建一个新文件
        with open(file_path, 'w') as file_obj:  
            json.dump(user_name, file_obj)
    else:
        print("hello " + user_name + "you are our existing user")


greeter()

greeter()
```


下面演示重构的一个基本思想：
* 函数1：`get_username(path)` 获取用户名，如果用户名存在于 json 文件中，那么返回文件内容；否则返回`None`
* 函数2：`create_newuser(name, path)` 如果不存在该用户时，创建一个新用户写入到 json 文件中
* 函数3：`greeter()` 总控程序
``` python
import json
file_path = 'username2.json'

def get_username(path):
    try:
        with open(path) as file_obj:
            return json.load(file_obj)
    except:
        return None


def create_newuser(name, path):
    with open(path, 'w') as file_obj:
        json.dump(name, file_obj)


def greeter():
    user_name = get_username(file_path)
    if user_name:
        print("hello " + user_name + " you are our old user")
    else:
        name = raw_input("your are new to this website pls input your name: ")
        create_newuser(name, file_path)
        print("welcome " + name + " to our website...")


greeter()
greeter()
```


