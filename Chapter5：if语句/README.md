# if 语句

## if 语句的语法格式
``` python
names = ['bob', 'alice', 'ally', 'peter']
for name in names:
    if name == 'alice'
        print('hi, i am alice...')
    else:
        print('i am not alice')
```

多个符合条件时，使用关键字`and`和`or`
``` python
age1 = 20
age2 = 10
if age1 >= 18 and age2 >= 18
    print('both greater equal than 18')
if age1 >= 18 or age2 >= 18
    print('there must be one value greater than 18')
```
## 检查某个值是否在列表中

* `in` : 在列表中
* `not in` : 不在列表中
``` python
names = ['alice', 'bob', 'tom', 'tim']
print('alice' in names)     #True
print('peterson' in names)  #False
```

## if-elif-else 结构

* python 中并不要求最终必须要有`else`条件代码块，一个好的习惯是：如果知道最终情况所需要满足的条件的话，那么最好使用`elif`显示的指出这个条件，而不是使用`else`模糊的说明，例子如下：
``` python
age = 66
if age < 4:
    price = 0
elif age < 18:
    price = 5
elif age < 65:
    price = 10
elif age >= 65:   # 显示的指出最后一种条件
    price = 5
print('the price is $' + str(price) + '.')
```

## 使用 if 来处理列表

* 可以将列表名放在条件表达式中，判断其是否为空列表
``` python
names = []
if names:
    print('names is empty')
else:
    print('name is not empty')
```
* 在 for 循环中使用 if 判断特殊的情况
``` python
available_toppings = ['mushrooms', 'olives', 'green peppers',
                        'pepperoni', 'pineapple', 'extra cheese']
requested_toppings = ['mushrooms', 'french fries', 'extra cheese']
for requested_topping in requested_toppings:
    if requested_topping in available_toppings:
        print("Adding " + requested_topping + ".")
    else:
        print("Sorry, we don't have " + requested_topping + ".")
print("\nFinished making your pizza!")

```

