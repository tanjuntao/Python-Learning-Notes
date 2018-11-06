# 类

## 创建和使用类
* python 中类名首字母大写，方法名小写
* `__init__(self,...)`这是一种约定，将构造方法和其他方法区分开来
* `__init__(self,...)`方法会返回一个实例,虽然其没有显示的指出`return`
``` python
class Dog(object):
    """monitor dog"""
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def sit(self):
        print(self.name.title() + "is sitting...")

    def roll(self):
        print(self.name.title() + "is rolling over "
                                  "and its age is " + str(self.age))

my_dog = Dog('alice', 6)
print(my_dog.name)
print(str(my_dog.age))
my_dog.sit()
my_dog.roll()

your_dog = Dog('bob', 1)
print(your_dog.name)
print(your_dog.age)
your_dog.sit()
your_dog.roll()
```
## 使用类和实例
* 如果要给某个属性一个默认值，那么可以将设置属性默认值的代码放在`__init()__`方法中

可以通过下面两种方式修改属性
1. 通过 `实例.属性` 的方式直接修改
2. 通过 `实例.方法` 的方式间接修改

下面的代码演示了这些方法：
``` python
class Person(object):
    def __init__(self, name, age, university):
        self.name = name
        self.age = age
        self.university = university
        self.hometown = "anqing anhui"   # default value of attribute 'hometown' is 'anqing anhui'

    def get_info(self):
        full_info = self.name + "'s age is " + str(self.age) + \
                    " and comes from " + self.university + " and hometown is " + self.hometown
        return full_info

    def update_age(self, new_age):
        if new_age > 30:
            print("i am not that old...")
            return
        else:
            self.age = new_age

me = Person('tanjuntao', '22', 'HFUT')
info = me.get_info()
print(info)
me.age = 23   # modify attribute by accessing it directly
print(me.get_info())

me.update_age(21) # modify attribute by calling a function
print(me.get_info())
```

## 继承

* 子类继承父类中所有的属性和方法
* 子类初始化`__init__(self)`方法时需要调用父类中的`__init__(self))`方法
* 子类继承父类时，必须在子类名括号中指明父类名
``` python
# 一般的格式 python2.7
class superclass_name(object):
    def __init(self, ...):
        ...
        ...
    def ...
        ...
        ...

class subclass_name(superclass_name):
    def __init(self, ...):
        super(subclass_name, self).__init(...)__
        ...
    def ...
        ...

instance_name = subclass_name(...)
```
* 可以重写从父类中继承而来的方法
* 可以在一个类中包含另一个类的实例，作为当前类的一个属性

演示：
``` PYTHON
class Animal(object):   # python2.7 must contain the argument 'object'
    def __init__(self, type, name):
        self.type = type
        self.name = name

    def info(self):
        return "type is " + self.type + " and name is " + self.name

class Dog(Animal):
    def __init__(self, type, name):
        super(Dog, self).__init__(type, name)    # call the superclass init function
        self.sound = 'wangwang'   # subclass's attribute not in the superclass

    def get_sound(self):          # subclass's method that not in the superclass
        return self.sound

my_dog = Dog('hashiqi', 'jiajia')
print(my_dog.info())

print(my_dog.get_sound())
```


## 导入类
* 对每个模块类，需要用`文档字符串`来描述这个模块的作用

1. 导入单个类
``` python
from module_name import class_name

instance_name = class_name(...)
```
2. 导入一个模块中多个类，每个类用`,`分隔开来
``` python
from module_name import class_name1, class_name2

instance_name1 = class_name1(...)
instance_name2 = class_name2(...)
```
3. 导入整个模块
``` python
import module_name
instance_name = module_name.class_name(...)
```
* 最推荐这种方式导入模块中的类，很清晰。
4. 导入模块中所有的类
``` python
from module_name import *
instance_name1 = class_name1(...)
instance_name2 = class_name2(...)
```
* **不推荐**！这种方式
    1. 不能清楚的说明导入了哪些类
    2. 容易和本文件中定义的类名发生冲突


## 有序字典

* 使用模块 `collections` 中的类 `OrderedDict`，调用其构造函数创建的字典实例，是有序字典

例子：
``` python
from collections import OrderedDict

# 列表的打印顺序是有序的
names = ['alice', 'bob', 'tanjuntao', 'xiaojun', 'peter', 'jordan']
for name in names:
    print(name)

# 普通字典打印顺序是无序的
favorite_languages = {}
favorite_languages['alice'] = 'python'
favorite_languages['bob'] = 'C++'
favorite_languages['tanjuntao'] = 'java'
favorite_languages['peter'] = 'javascript'
for name, language in favorite_languages.items():
    print(name + " " + language)

# 使用类 OrderedDict 创建实例（一个字典），打印顺序是有序的
ordered_favo_languages = OrderedDict()
ordered_favo_languages['alice'] = 'python'
ordered_favo_languages['bob'] = 'C++'
ordered_favo_languages['tanjuntao'] = 'java'
ordered_favo_languages['peter'] = 'javascript'

for name, language in ordered_favo_languages.items():
    print(name + " " + language)
```

## 类的编码风格
* 类名使用`驼峰命名法`，每个单词首字母大写，不使用下划线连接
* 实例名和模块名使用`小写字母+下划线`的方式命名
* 每个类后面跟文档字符串，来描述这个类的功能;每个模块也同样要包含一个文档字符串
* 在类中，用`一个空行`来分隔方法
* 在模块中，用`两个空行`来分隔类
* 先导入标准库模块，接着空一行，再导入自己编写的模块