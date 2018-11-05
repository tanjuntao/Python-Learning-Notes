# 变量和简单数据类型
## 变量
* 谨慎使用小写字母`i`和`o`，因为容易被看错成为`1`和`0`
* 建议使用小写的 python 变量名
* `NameError`一般原因是：变量没有赋值；s呼入的变量名拼写不正确
* python 文件名建议使用 `小写字母+下划线` 的方式


## 字符串
* 字符串可以用单引号括起来也可以用双引号括起来
``` python
'i told my friend "python is the best language"'
"the language 'python' is the best"
```
* 即可以在双引号中间添加单引号，不需要使用转义字符等等


几个常用的方法
* `title()`：将每个单词转换为首字母大写的形式
* `capitalize()`同上
* `upper()`将所有的字母全部转为大写
* `lower()`将所有的字母全转为小写
* `rstrip()`去除字符串右边的空白，`r`表示`right`
* `lstrip()`去除字符串左边的空白，`l`表示`left`
* `strip()`去除字符串左右两边的空白



## 数字
* python 中的平方用`**`表示
``` python
2 ** 3 = 8
3 ** 2 = 9
10 ** 3 = 1000
```
* `str(integer)`函数将整数转换为字符串形式如：
``` python
age = 22;
message = "happy" + str(age) + "ed Birthday!"
```
* python 中两个整数相除同样是只保留整数部分，舍弃小数部分
``` python
3 / 2 = 1
3.0 / 2 = 1.5
3 / 2.0 = 1.5
```


