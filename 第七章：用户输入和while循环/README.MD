# 用户输入和 while 循环

## raw_input() 函数
注：  
* `input()函数`：python3中使用
* `raw_input()函数` python2中使用
* 在 python2 中获取输入使用`raw_input()函数`，不要使用`input()函数`，很容易出错

`raw_input()函数` 接受一个参数，是`一段提示性文本`，提示用户输入什么。

* `int()函数` 将数值类型的字符串转换为整型
``` python
value = '222'
print(value)    # 输出'222'
value = int(value)
print(value)    # 输出 222
```

## 使用 while 循环处理列表和字典

* 在列表之间移动元素
``` python
# 将未验证的用户逐个添加到验证用户列表中
unverified_users = ['alice', 'bob', 'tom', 'tim', 'tein']
verified_users = []
while unverified_users:
    current_user = unverified_users.pop()
    print("verifying " + current_user)
    verified_users.append(current_user)

print("\nall verified users are")
for user in verified_users:
    print(user)
```

* 删除列表中所有重复出现的元素
``` python
names = ['alice', 'bob', 'tom', 'alice', 'peter', 'alice']
while 'alice' in names:
    names.remove('alice')

print(names)
```

* 使用用户输入来填充字典
``` python
persons = {}
active = True
while active:
    firstname = raw_input('input your firstname: ')
    age = input('input your age: ')
    persons[firstname] = age
    message = raw_input("would your want to add another persons' info?(Y/N): ")
    if message == 'N':
        active = False

print(persons)
```

