## Python 中文编码

在Python文件中如果未指定编码格式，则默认ASCII编码。此时如果输出中文字符，则会报错（SyntaxError）。

解决方法为在文件开头加入以下内容：

① 写法一：

```
# coding = utf-8
```

② 写法二：

```
 # -*- coding: UTF-8 -*-
```

## Python 指定解释器路径

* 若使用`python xx.py`运行Python程序，可以不写解释器路径；  
* 若使用`./xx.py`运行Python程序，则要写解释器路径

① 写法一：

```
#!/usr/bin/env python
```

**推荐使用写法一。**  
用写法一可以在你安装多版本Python时，取PATH中第一个Python执行；若配置了虚拟环境，也可以保证你用虚拟环境中的Python执行

② 写法二：

```
#!/usr/bin/python
```

默认的Python解释器的路径

## Python 变量类型

### Python 列表

List（列表） 是 Python 中使用最频繁的数据类型。

* 列表可以完成大多数集合类的数据结构实现。它支持字符，数字，字符串甚至可以包含列表（所谓嵌套）。
* 列表用\[ \]标识。是python最通用的复合数据类型。看这段代码就明白。
* 列表中的值得分割也可以用到变量\[头下标:尾下标\]，就可以截取相应的列表，从左到右索引默认0开始的，从右到左索引默认-1开始，下标可以为空表示取到头或尾。
* 加号（+）是列表连接运算符，星号（\*）是重复操作。如下实例：

  ```
    # coding = utf-8

    list = [ 'runoob', 786 , 2.23, 'john', 70.2 ]
    tinylist = [123, 'john']

    print list               # 输出完整列表
    print list[0]            # 输出列表的第一个元素
    print list[1:3]          # 输出第二个至第三个的元素 
    print list[2:]           # 输出从第三个开始至列表末尾的所有元素
    print tinylist * 2       # 输出列表两次
    print list + tinylist    # 打印组合的列表
  ```

以上实例输出结果：

```
['runoob', 786, 2.23, 'john', 70.2]
runoob
[786, 2.23]
[2.23, 'john', 70.2]
[123, 'john', 123, 'john']
['runoob', 786, 2.23, 'john', 70.2, 123, 'john']
```

### Python元组

元组是另一个数据类型，类似于List（列表）。

* 元组用"\(\)"标识。内部元素用逗号隔开。但是元组不能二次赋值，相当于只读列表。

```
# coding = utf-8

tuple = ( 'runoob', 786 , 2.23, 'john', 70.2 )
tinytuple = (123, 'john')

print tuple               # 输出完整元组
print tuple[0]            # 输出元组的第一个元素
print tuple[1:3]          # 输出第二个至第三个的元素 
print tuple[2:]           # 输出从第三个开始至列表末尾的所有元素
print tinytuple * 2       # 输出元组两次
print tuple + tinytuple   # 打印组合的元组
```

以上实例输出结果：

```
('runoob', 786, 2.23, 'john', 70.2)
runoob
(786, 2.23)
(2.23, 'john', 70.2)
(123, 'john', 123, 'john')
('runoob', 786, 2.23, 'john', 70.2, 123, 'john')
```

以下是元组无效的，因为元组是不允许更新的。而列表是允许更新的：

```
# coding = utf-8

tuple = ( 'runoob', 786 , 2.23, 'john', 70.2 )
list = [ 'runoob', 786 , 2.23, 'john', 70.2 ]
tuple[2] = 1000    # 元组中是非法应用
list[2] = 1000     # 列表中是合法应用
```

### Python 元字典

字典\(dictionary\)是除列表以外python之中最灵活的内置数据结构类型。列表是有序的对象结合，字典是无序的对象集合。

* 两者之间的区别在于：字典当中的元素是通过键来存取的，而不是通过偏移存取。
* 字典用"{ }"标识。字典由索引\(key\)和它对应的值value组成。

  ```
    # coding = utf-8

    dict = {}
    dict['one'] = "This is one"
    dict[2] = "This is two"

    tinydict = {'name': 'john','code':6734, 'dept': 'sales'}

    print dict['one']          # 输出键为'one' 的值
    print dict[2]              # 输出键为 2 的值
    print tinydict             # 输出完整的字典
    print tinydict.keys()      # 输出所有键
    print tinydict.values()    # 输出所有值
  ```

输出结果为：

```
This is one
This is two
{'dept': 'sales', 'code': 6734, 'name': 'john'}
['dept', 'code', 'name']
['sales', 6734, 'john']
```

## Python 运算符

### Python算术运算符

以下假设变量a为2，变量b为3：

| 运算符 | 描述 | 实例 |
| --- | --- | --- |
| \*\* | 幂 - 返回x的y次幂 | a\*\*b 为2的3次方，输出结果 8 |
| // | 取整除 - 返回商的整数部分 | a//b 输出结果 0 , b//a 输出结果 1 |

**注意：Python中没有**`++`**和**`--`**的自增/减运算符**  
**拓展：为什么Python、Ruby中没有自增/减运算符？**

* 在Python中有`a += 1`，没有`a++`。
* `a += 1`改变了变量，表达式新建了个对象，把`a+1`的结果存在这个对象中，然后将引用a指向该对象，使得变量a改变。
* `a++`改变了对象本身（直接对对象进行`++`），这个对象指的是内存中存放基本类型的数据的地址所指的内容。
* 在 Python 中，数值对象是一种不可变类型。在创建对象之后，其值就不能再被改变。

### Python比较运算符

以下假设变量a为10，变量b为20：

| 运算符 | 描述 | 实例 |
| --- | --- | --- |
| &lt;&gt; | 不等于 - 比较两个对象是否不相等 | \(a &lt;&gt; b\) 返回 true。这个运算符类似 != |

### Python赋值运算符

以下假设变量a为10，变量b为20：

| 运算符 | 描述 | 实例 |
| --- | --- | --- |
| \*\*= | 幂赋值运算符 | c **= a 等效于 c = c ** a |
| //= | 取整除赋值运算符 | c //= a 等效于 c = c // a |

### Python逻辑运算符

Python语言支持逻辑运算符，以下假设变量 a 为 10, b为 20:

| 运算符 | 逻辑表达式 | 描述 | 实例 |
| --- | --- | --- | --- |
| and | x and y | 布尔"与" - 如果 x 为 False，x and y 返回 False，否则它返回 y 的计算值。 | \(a and b\) 返回 20。 |
| or | x or y | 布尔"或"    - 如果 x 是非 0，它返回 x 的值，否则它返回 y 的计算值。 | \(a or b\) 返回 10。 |
| not | not x | 布尔"非" - 如果 x 为 True，返回 False 。如果 x 为 False，它返回 True。 | not\(a and b\) 返回 False |

### Python成员运算符

除了以上的一些运算符之外，Python还支持成员运算符，测试实例中包含了一系列的成员，包括字符串，列表或元组。

| 运算符 | 描述 | 实例 |
| --- | --- | --- |
| in | 如果在指定的序列中找到值返回 True，否则返回 False。 | x 在 y 序列中 , 如果 x 在 y 序列中返回 True。 |
| not in | 如果在指定的序列中没有找到值返回 True，否则返回 False。 | x 不在 y 序列中 , 如果 x 不在 y 序列中返回 True。 |

### Python运算符优先级

以下表格列出了从最高到最低优先级的所有运算符：

| 运算符 | 描述 |
| --- | --- |
| \*\* | 指数 \(最高优先级\) |
| ~ + - | 按位翻转, 一元加号和减号 \(最后两个的方法名为 +@ 和 -@\) |
| \* / % // | 乘，除，取模和取整除 |
| + - | 加法减法 |
| &lt;&lt; &gt;&gt; | 左移，右移运算符 |
| & | 位 'AND' |
| ^ \| | 位运算符 |
| &lt;= &lt; &gt; &gt;= | 比较运算符 |
| &lt;&gt; == != | 等于运算符 |
| = %= /= //= -= += _= \*_= | 赋值运算符 |
| is is not | 身份运算符 |
| in not in | 成员运算符 |
| not or and | 逻辑运算符 |

## Thanks

> \[Python语法\] [http://www.runoob.com/python/python-tutorial.html](http://www.runoob.com/python/python-tutorial.html)  
> \[Python教程\] [http://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000](http://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000)  
> \[Python中为什么没有++和--（自增/减）\] [http://blog.csdn.net/guang09080908/article/details/47273765](http://blog.csdn.net/guang09080908/article/details/47273765)  
> \[为什么 Python、Ruby 等语言弃用了自增运算符？\] [https://www.zhihu.com/question/20913064](https://www.zhihu.com/question/20913064)



