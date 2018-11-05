# 字典

## 使用字典
* 字典就是一些列的`键-值对`，与键关联的值可以是`数字` `字符串` `列表` `另一个字典`。可以将 python 中的任何一种对象作为字典的值。
* 字典是一种动态结构，可以随时添加更多的键值对。不需要使用类似于列表中的`append()函数`，直接使用赋值运算：
    ``` python
    alian = ['color':'green', 'points', 5]
    print(alian)
    alian['x_pos'] = 0  # 添加了一个键值对
    alian['y_pos'] = 25 # 再添加一个键值对
    print(alian)
    ```
* **键值对的打印顺序可能和添加顺序不同，python中不关心添加顺序，只关心键值对之间的关联关系**
* 删除键值对：`del alian['color']`,永久删除
* 字典可以存储的是一个实体（例如人）的多种信息（多个属性），同样的，字典也可以存储同一类信息，如将所有人以及其喜欢的编程语言存储到一个字典中。

## 遍历字典

首先创建一个字典，其中包含的是每个人和其喜欢的编程语言：
``` python
favorite_languages = {
    'alice':'python',
    'bob':'java',
    'peter':'C++',
    'tom':'ruby',
}
```
1. 遍历所有的键值对，调用`items()`
``` python
for name, language in favorite_languages.items():
    print(name)
    print(language)
```

2. 遍历所有的键，调用`keys()`，如果要求键按要求排序，那么可以进一步调用函数`sorted()`临时排序
``` python
for name in favorite_languages.keys():
    print(name)

# 如果不显示指明函数keys()的话，直接使用字典名也是可行的
for name in favorite_languages:
    print(name)

#对所有的键临时排序
for name in sorted(favarite_languages.keys()):
    print(name)
```
* 函数`keys()`其实是返回了一个列表，这个列表包含了字典中所有的键，因此可以使用关键字`in`来判断某个值是否在列表中
``` python
if 'alice' in favarite_languages.keys():
    print('yes!')
```

3. 遍历所有的值，使用函数`values()`，如果要求所有的值不重复的话，可以使用集合set，即进一步调用函数`set()`
``` python
for language in favorite_languages.values():
    print(language)

# 返回的值结果不重复
for language in set(favorite_languages.values()):
    print(language)
```

* 注：**以上所有的遍历方式中，返回的结果都是不确定的，即不和原先字典中键值对的排列顺序相同。python 的理念是关注键值的对应情况，而不关心排列顺序。**



## 嵌套
1. 列表中嵌套字典
    * 列表中的每个元素都是一个字典
``` python
all_users = []
for number in range(0, 30):
    new_alian = {'color':'yellow', 'points':5}
    all_users.append(new_alian)
```

2. 字典中嵌套列表
    * 键值对中的每个值是一个列表，需要使用循环才能遍历这个值
``` python
favorite_languages = {
    'alice':['python', 'c'],
    'bob':['java', 'python'],
    'peter':['perl', 'ruby'],
    'tom':['c++', 'matlab'],
    'tim':['javascript']
}

for name, languages in favorite_languages.items():
    if len(languages) == 1:
        print(name + "'s favorite language is: " + languages[0])
    else:
        print(name + "'s favorite languages are")
        for language in languages:
            print("\t" + language)
```

3. 字典中嵌套字典
    * 键值对中每个值都是另外一个字典
``` python
all_user = {
    'usiatein':{
        'firstname':'tan',
        'secondname':'juntao',
        'university':'hfut'
    },
    'teintein':{
        'firstname':'tan',
        'secondname':'xiaojun',
        'university':'ustc'
    },
}

for username, info in all_user.items():
    print('user name is ' + username)
    full_name = info['firstname'] + " " + info['secondname']
    print('\tfull name is ' + full_name)
    print('\tuniversity is ' + info['university'])

```
* 注：嵌套的字典，结构最好要保持一致，这样在使用 for 循环时，可以使用统一的代码来处理嵌套的字典。