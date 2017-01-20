# 1.说明
- 参考来源：[Google Python Style Guide](https://google.github.io/styleguide/pyguide.html)
- [中文翻译](http://zh-google-styleguide.readthedocs.io/en/latest/google-python-styleguide/python_language_rules/)
- 文档未尽内容，可以参考上述文档
# 2.常用内容列举
## 缩进
使用4个空格缩进代码，绝对不要使用tab，也不要tab和空格混用
```
Yes:
foo = long_function_name(var_one,var_two,
                         var_thress,var_four)
```
```
No:
 foo = long_function_name(var_one, var_two,
          var_three, var_four)
```
## 全局变量及常量
全局变量主要指模块级别，所有字母大写,单词之间以`_`连接（GLOBAL_VAR_NAME），避免使用全局共享变量，推荐使用类变量
```
class A(object):
    count = 0#类变量
    def __init__(self)

```
常量 PI = 3.14，全部大写，单词下滑线连接
## 命名
`package_name,module_name,ClassName,methode_name,function_name,GLOBAL_VAR_NAME,instance_var_name,function_parameter_name,local_var_name`
module_name没必要和类名保持一致，也不是一个module只能包含一个类
## 导入包和模块
导入时不要使用相对名称，即使模块在同一个包中
## 列表推导
简单情况可以使用列表推导，复杂逻辑建议还是使用循环
## 生成器
生成器函数中不能使用return
## 函数默认参数
在函数参数列表的最后指定变量的值
```
def foo(a,b=0) #正确
def foo(a,b=0,c) #错误
```
## True/False
python 中所有的"空"值被认为是false，即0，None，[],{}
```
x = 0 #None,[],{}
if x:
    print 'yes' #not execute
```
## 注释
在python中注释有两种：一种是doc string，一种是comment
### doc string
形式如："""xxxx"""，会生成文档（__doc__）,理论上一个函数或类必须有doc string(说明)，除非它非常简单明了
#### 函数注释
```
def fetch_bigtable_rows(big_table, keys, other_silly_variable=None):
    """Fetches rows from a Bigtable.

    Retrieves rows pertaining to the given keys from the Table instance
    represented by big_table.  Silly things may happen if
    other_silly_variable is not None.

    Args:
        big_table: An open Bigtable Table instance.
        keys: A sequence of strings representing the key of each table row
            to fetch.
        other_silly_variable: Another optional variable, that has a much
            longer name than the other args, and which does nothing.

    Returns:
        A dict mapping keys to the corresponding table row data
        fetched. Each row is represented as a tuple of strings. For
        example:

        {'Serak': ('Rigel VII', 'Preparer'),
         'Zim': ('Irk', 'Invader'),
         'Lrrr': ('Omicron Persei 8', 'Emperor')}

        If a key from the keys argument is missing from the dictionary,
        then that row was not found in the table.

    Raises:
        IOError: An error occurred accessing the bigtable.Table object.
    """
    pass
```
#### 类注释
类应该在其定义下有一个用于描述该类的文档字符串，如果类具有公共属性(Attributes),那么文档中应该有一个属性字段，描述参数作用
```
class SampleClass(object):
    """Summary of class here.

    Longer class information....
    Longer class information....

    Attributes:
        likes_spam: A boolean indicating if we like SPAM or not.
        eggs: An integer count of the eggs we have laid.
    """

    def __init__(self, likes_spam=False):
        """Inits SampleClass with blah."""
        self.likes_spam = likes_spam
        self.eggs = 0

    def public_method(self):
        """Performs operation blah."""
```
### comment 
块注释或行注释，使用`#`
```
# We use a weighted dictionary search to find out where i is in
# the array.  We extrapolate position based on the largest num
# in the array and the array size and then do binary search to
# get the exact number.

if i & (i-1) == 0:        # true iff i is a power of 2
```
## 线程
线程间交换数据尽量使用Queue module，使用内建类型比如字典等实际上不具有原子性，注意使用锁