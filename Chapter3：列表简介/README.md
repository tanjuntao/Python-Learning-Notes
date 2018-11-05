# 列表简介
## 列表是什么
* 列表变量的名称一般使用复数表示，如`names` `letters` `digis`
* 列表的索引是从`0`开始而不是从`1`开始，和matlab中的矩阵向量不一样
* 如何快速访问列表中的最后一个元素呢？
``` python
names = ['Alice', 'Bob', 'Mike', 'Justin']
print(names[-1])  #输出 Justin
print(names[-2])  #输出 Mike
```

## 插入、删除、修改
* python 中的列表是动态的
``` python
names = ['Alice', 'Bob', 'Mike', 'Justin']

# 在列表尾部插入元素
names.append('Johnson')
# 一般是创建一个空列表，然后动态的往里面添加元素
digits = []
digits.append(1)
digist.append(2)

# 使用insert函数往列表中任意位置插入元素
names.insert(1, 'James')  #插入到第二个位置，其它元素后移

# 使用del来删除元素
del names[2]  #删除第三个元素

# 使用pop来弹出元素，并且操作这些弹出的元素
last_name = names.pop()   #弹出列表中最后一个元素，并且赋值给变量

# 也可以使用pop弹出任何一个位置的元素
name = names.pop(2)  #弹出第三个位置的元素，并且赋值给name

# 使用remove来删除指定值的元素
names.remove('James')  #删除元素值为 James 的元素
```

几点需要注意的地方
1. `remove()`函数只负责删除列表中的一个元素，如果要删除多个，那需要使用到while循环
2. 如果只删除元素，不需要使用这些元素，那么使用`del`;如果删除之后还要利用这些被删除的元素，那么使用`pop()`
3. 只有`del`的使用方式是`del names(2)`这种，其它的函数都是使用`.`运算符，如`names.remove('James')`



## 组织列表

几个函数
* `sort()`对列表永久性排序，无法恢复原先列表
* `sort(reverse=True)`对列表永久性排序，但是以元素大小倒序的方式排列
* `sorted()` 对列表临时排序，不影响原先列表的元素顺序
* `sorted(reverse=True)` 对列表临时排序，按照元素值大小倒叙的方式排列
* `reverse()` 将列表倒叙，永久性的更改，但是可以再一次调用`reverse()`还原原先的列表
* `len()` 返回列表的长度

