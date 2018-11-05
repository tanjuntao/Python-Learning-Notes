# 操作列表

## 遍历整个列表
使用 for 循环
``` python
names = ['alice', 'bob', 'mike', 'johnson', 'tein']
for name in names:
    print(name)
```
* 好习惯：列表名用复数形式，用于循环遍历的变量使用单数。

## 避免缩进错误
下面是一段逻辑错误的代码
``` python
names = ['alice', 'bob', 'mike', 'johnson', 'tein']
for name in names:
    print(name)
print("can't wait to see your next show " + name + "\n")
```
* 本来是想对于每个元素都打印一条语句，结果由于没有缩进，最后只在 for 循环结束后执行了一次
* 由于 for 循环最后的值是 `tein`,因此最后打印的语句中包含的值就是 `tein`
* **for循环后面别忘了冒号**

## 创建数值列表
* range(1, 5)包含的是值是`1~4`不是`1~5`，不包含结束元素
* 创建一个数值列表
``` python
numbers = list(range(1,6))
print(numbers)  #输出结果是[1,2,3,4,5]
```
* `range(2,11,2)` range 函数的第三个参数值*步长*，


构建一个列表  
1. 可以使用 *for循环* 的方式
``` python
values = []
for value in range(1, 11)
    values.append(value ** 2)
```
2. 也可以使用*列表解析* 的方式
``` python
values = [value ** 2 for value in range(1, 11)]
```

几个函数
* `max(values)` 返回数字列表的最大值
* `min(values)` 返回数字列表的最小值
* `sum(values)` 返回数字列表所有元素的和


## 切片

集中使用切片的方法
* `values[1:4]` 取出从索引`1`到`3`的元素，和`range(1,4)`一样，都不包含最后一个元素
* `values[:3]` 没有指定第一个索引，那么从列表开头开始
* `values[3:]` 没有指定第二个索引，那么取到列表最后一个元素
* `values[-3:]` 取列表最后三个元素
* `values[-4:]` 同上，取列表最后四个元素
* 使用 for 循环遍历切片，因为切片也是一个列表
* 切片的一个应用是：*网页程序中会用切片来分页显示信息*

复制切片的两种方式
1. 完全复制（类似于值复制）
``` python
values1 = list(range(1, 11))

values2 = values[:]  # 值复制

values1.append(100)
values2.append(200)
print(values1)  # 值为[1,2...10,100]
print(values2)  # 值为[1,2...10,200]
```
2. 引用复制（两个变量名指向同一个列表）
``` python
values1 = list(range(1, 11))

values2 = values1

values1.append(100)
values2.append(200)
print(values1)  # 值为[1,2...10,100,200]
print(values2)  # 值为[1,2...10,100,200]
```
* 第一种赋值中，是完全两个列表；但是第二种赋值中，是同一个列表，两个变量名虽然不同，但是指向的是同一个列表


## 元组
* 列表中的值是可以通过赋值运算来修改的，但是元组中的值是不能通过赋值来修改的
* 元组的遍历和列表一样
* 可以通过重新初始化元组来改变其值
``` python
values = (1,2,3)
for value in values:
    print(value)
# values[1] = 100  这是禁止的，不能通过赋值运算来改变元组的值
values = (3,4,5)  # 但是可以通过重新声明来改变其值
```

## PEP8 指南

几点代码格式要求
* 缩进采用4个字符
* 行长不超过80个字符
