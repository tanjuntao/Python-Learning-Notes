# 测试代码


## 测试函数
* 需要使用 python 标准库中的 `unittest` 模块
* 要编写测试用例，那么需要创建一个`测试类`，这个类继承`unittest.TestCase`，然后编写一系列的`方法`来测试函数不同的方面
* 编写的测试方法一定都得是`test_`打头的，这样 python 能够自动运行它，不需要手动编写调用函数的代码
* 使用`断言方法`来判断结果和预期是否一致

下面是一个测试例子：    

待测试函数`get_fullname`
``` python
def get_fullname(first, last, middle=''):
    if middle != '':
        return (first + ' ' + middle + ' ' + last).title()
    else:
        return (first + ' ' + last).title()
```

测试类 `NameTestCase`
``` python
import unittest  # 导入 unittest 模块
from module import get_fullname  # 导入被测试函数

class NameTestCase(unittest.TestCase):
    # 为函数第一种行为编写的测试方法
    def test_first_last_name(self):
        full_name = get_fullname('tan', 'juntao')
        self.assertEqual(full_name, 'Tan Juntao')

    # 为函数第二种行为编写的测试方法
    def test_first_middle_last_name(self):
        full_name = get_fullname('taylor', 'swift', 'alison')
        self.assertEqual(full_name, 'Taylor Alison Swift')

# 自动运行所有的test方法
unittest.main()
```

## 测试类
* 类的测试本质还是对类中的方法进行测试

`unittest`模块中一些常用的`断言方法`   

方法 | 用途
---- | ---
`assertEqual(a, b)`  | 核实 a == b
`assertNotEqual(a, b)`  | 核实 a != b
`assertTrue(x)`  |  核实 x 为 True
`assertFalse(x)`   |  核实 x 为 False
`assertIn(item, list)`  |  核实 item 在 list 中
`assertNotIn(item, list)`  | 核实 item 不在 list 中


下面演示一个测试类的例子

被测试类：
``` python
class AnonymousSurvey():
    def __init__(self, question):
        self.question = question
        self.responses = []

    # 显示问题
    def show_questions(self):
        print(self.question)

    # 添加回答
    def add_response(self, new_response):
        self.responses.append(new_response)

    # 显示所有的回答
    def show_responses(self):
        for response in self.responses:
            print("- " + response)
```

需要编写一个继承`unittest.TestCase`的类来完成测试
``` python
import unittest
from module import AnonymousSurvey

class TestAnonymousSurvey(unittest.TestCase):
    # 测试包含一个回答的情况
    def test_store_single_response(self):
        question = "what language do you speak? "
        survey = AnonymousSurvey(question)
        survey.add_response("english")

        self.assertIn("english", survey.responses)

    # 测试包含三个回答的情况
    def test_store_three_responses(self):
        question = "what language do you speak? "
        survey = AnonymousSurvey(question)
        responses = ['english', 'chinese', 'japanese']
        # 添加三个回答
        for response in responses:
            survey.add_response(response)
        # 测试三个回答是否都在列表中
        for response in responses:
            self.assertIn(response, survey.responses)

# 启动测试
unittest.main()
```

上述测试存在的问题：
* 每一个测试方法中，都有一个被测试类的实例。*能不能只需要一个实例，然后在不同的测试方法中使用同一个实例呢？*
* 答案是可以！使用`setUp()方法`
* 将实例化对象的操作放在`setUp()方法`中，这样 python 将会先调用`setUp()方法`，然后再调用各个`test_`开头的测试方法。

修改后的测试类如下
``` python
import unittest
from module import AnonymousSurvey

class TestAnonymousSurvey(unittest.TestCase):
    # 通过setUp()完成实例化
    def setUp(self):
        question = "what language do you speak? "
        self.survey = AnonymousSurvey(question)
        self.responses = ['english', 'chinese', 'japanese']

    def test_store_single_response(self):
        self.survey.add_response(self.responses[0])
        self.assertIn(self.responses[0], self.survey.responses)


    def test_store_three_responses(self):
        for response in self.responses:
            self.survey.add_response(response)

        for response in self.responses:
            self.assertIn(response, self.survey.responses)

unittest.main()
```
