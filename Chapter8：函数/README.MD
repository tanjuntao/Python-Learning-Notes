# 函数

* ```"""这是文档字符串"""``` 用三个双引号括起来的也是注释，只是这种注释用于生成 python 文档


## 传递实参
1. 位置实参
``` python
def info(firstname, lastname):
    print('my full name is ' + firstname + ' ' + lastname)

info('tan', 'juntao')
info('tan', 'xiaoju')
```
* python 将按照顺序将实参映射到形参

2. 关键字实参
* 在调用函数时，明确指明函数形参的值是什么，这时候可以不用像位置实参那样严格遵守形参的顺序，因为 python 知道每个值对应什么形参
``` python
def info(firstname, lastname):
    print('my full name is ' + firstname + ' ' + lastname)

info(firstname='tan', lastname='juntao')
info(lastname='juntao', firstname='tan')
```
3. 默认值
* 可以在定义函数时，给某个形参指定一个默认值，这样在调用函数时，如果没有指定该形参的值，那么就使用默认值作为形参的值
* 使用默认值时，必须将没有使用默认值的形参放在第一个位置上，将使用了默认参数的形参放在后面，这样在调用时，可以将指明了实参的值映射到前面的形参上，而使得后面的形参使用默认值。
``` python
def info(firstname, lastname='juntao'):
    print('my full name is ' + firstname + ' ' + lastname)

info('tan')
info('xu')
```
4. 几种完全等效的函数调用
``` python
def info(firstname, lastname='juntao'):
    print('my full name is ' + firstname + ' ' + lastname)

# tan juntao
info('tan')
info('tan', 'juntao')

# tan xiaojun
print('\n')
info('tan', 'xiaojun')
info(firstname='tan', lastname='xiaojun')
info(lastname='xiaojun', firstname='tan')
```

## 返回值
1. 让实参变成是可选的：使用默认参数。
``` python
def info(firstname, lastname, middlename = ''):
    if middlename:
        return firstname + " " + middlename + " " + lastname
    else:
        return firstname + " " + lastname

print(info('tan', 'juntao'))
print(info('tan', 'juntao', 'middle'))
```
* 可以使用`字符串`作为`条件表达式`，**如果字符串不为空，那么返回True；如果字符串为空，那么返回False**
* 之前的例子中，也可以将列表名作为条件表达式，如果列表为空，那么表达式值为 False

2. 返回一个字典
``` python
def info(firstname, lastname, age=''):
    person = {'first':firstname, 'last':lastname}
    if age:
        person['age'] = age
    return person

print(info('tan', 'juntao', 22))
```

## 传递列表
* 在函数内部修改了列表之后，对这个列表来说将是永久性的，形参不是列表的一个副本，就是实参的那个列表  

下面这段代码演示了如何使用函数来组织两个列表之间的元素转移。
``` python
def tranfer(list1, list2):
    while list2:
        temp = list2.pop()
        print(temp)
        list1.append(temp)

def print_all(list):
    for item in list:
        print(item)

list1 = ['alice', 'bob', 'peter']
list2 = []
tranfer(list2, list1)
print(list2)
```

* 可以使用`list1[:]`这种方式来传递列表的副本，这样原来的列表不受函数调用的影响
``` python
def tranfer(list1, list2):
    while list2:
        temp = list2.pop()
        print(temp)
        list1.append(temp)

def print_all(list):
    for item in list:
        print(item)

list1 = ['alice', 'bob', 'peter']
list2 = []
tranfer(list2, list1[:])  # 使用列表的副本，list1不受影响
print(list1)
tranfer(list2, list1)     # 使用原本的列表，函数调用结束后list1的值发生变化
print(list1)
```
**注意：如果是用列表的副本来调用函数，那么将需要大量的内存来开辟副本空间，不推荐。所以除非是有特殊的要求才会使用列表副本，否则的话还是应该讲原先列表传递给函数。**

## 传递任意数量的关键字实参
* 在形参前面加一个`*`号，那么 python 将创建一个元组，这个元组中包含了所有用户提供的实参，如下面的`*names`
``` python
def show_names(*names):
    for name in names:
        print('- ' + name)

# 可以只提供一个实参
show_names('tanjuntao')
# 也可以提供多个实参 
show_names('alice', 'bob', 'mike', 'tom')
```

* 在形参前面加一个`**`号，那么 python 将会创建一个字典，这个字典中包含的是用户提供的所有的键值对，如下面的`**user_info`
``` python
def build_user(firstname, lastname, **user_info):
    profile = {}
    profile['first'] = firstname
    profile['last'] = lastname
    for key, value in user_info.items():
        profile[key] = value
    return profile

user = build_user('tan', 'juntao', home='anqing', university='hfut')
print(user)
```

* 注意，在传递键值对时，键不需要用引号括起来，因为其代表的是关键字实参


## 将函数存储在模块中
* 可以将函数单独存储在一个 `.py` 文件中，然后在另外一个文件中导入这个 `模块`
1. 导入整个模块
``` python
import module_name  # 导入模块中所有的函数，模块名等于文件名
module_name.function_name(...)
```

2. 导入特定函数
``` python
from module_name import function_name1, function_name2, ...
function_name(...)  # 前提是这个导入的函数和本文件中定义的函数名不冲突
```

3. 使用`as`来重命名函数或者模块
``` python
from module_name import function_name as fn  # 重命名函数，不能和本文件中的函数重名
fn(...)

import module_name as mn  # 重命名模块
mn.function_name(...)
```
4. 导入模块中所有的函数
``` python
from module_name import *  # 导入模块中所有的函数
....
```
* **不建议这么做**！如果模块函数很多，那么很容易和本文件中的函数重名，那么将会导致模块中的函数被覆盖，没有达到引用模块的目的。


## 函数编写规范
* 函数名和模块名都应该使用 `小写字母+下划线` 的方式来命名
* 在每个函数定义后，使用`文档字符串`来说明函数的作用
* 形参默认值等号两边**不要有空格**
* 关键字实参的等号两边也**不要有空格**
* 不同的函数之间用**两个空行**分隔
* 函数形参比较多时，可以在函数定义中输入左括号后回车，并在下一行按**两次 tab 键**，将形参缩进
