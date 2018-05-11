1. basic
    - 多行语句用\，但[], {} 或 () 之间的内容就不需要\
    - 用 '，"，'''，"""表示字符串，其中后两个可以跨行
    - expr与stmt之间用 :隔开
    - 第一行指定解析器：#!/usr/bin/python和#!/usr/bin/env python
    - 编码方式：#coding=utf-8
    - Python的内存管理机制是引用计数，内存回收时还会用到循环垃圾收集器
    - 空值为None
    - 在memory中的格式为unicode，在磁盘和网络中的格式为utf8
    - a = 1 if False else 3
2. scalar
    - 标准类型：int, long, float, complex, str, bytes, list, set, dict, tuple, slice, ‘function’, types中含有更多类型
    - numbers, str, bytes, tuple, slice是数值类型，不可变，其它则为引用类型，可变
    - 变量无类型
    - a, b, c = 1, 2, "john"
    - del a, b, c
    - 下标：[start, end, interval], 不包括上界，上下界可省，可双向，下界较小时，间隔要负，否则要正
    - range(start, end, interval)参数意义和下标一致
    - 对于str，*是重复操作
    - 类型转换为行为式
    - tuple不能更新
    - 用，隔开的对象默认为tuple
    - (), (1,)
3. operator
    - **为幂值
    - //为商的整数部分
    - and，or，not，in，not in，is，is not
    - id(o), 整数会复用内存
8. str
    - r/R'abc'：去转义
    - 'abc'%tuple
8. list
    - [m + n for m in 'ABC' for n in 'XYZ']
    - [x for x in range(1, 11) if x % 2 == 0]
8. dict
    - key可以是numbers， str， tuple，及自定义的对象
    - dict['a']不存在的话会抛出异常
    - del dict['a'],dict.pop('a'), dict.clear()
8. function
    - 参数类型为：必备参数，可变参数，关键字参数，默认参数
    - *和*arg后的参数均为关键字参数
    - *参数的传入可以是展开的1, 2, 3, 也可以是聚合的*(1, 2, 3), *[1, 2, 3], **也一样
    - 在函数内部使用全局变量要加上global
    - 可在函数中定义函数
    - lambda主体是一个表达式
    - 方法和函数可以互相转换
    - 尾递归优化：函数结尾调用自身
    - generator在for中不会产生except，也不会获取到返回值，用next会产生except，也会获取到返回值
    - 凡是可作用于for循环的对象都是Iterable类型，可用iter()变成Iterator
    - 凡是可作用于next()函数的对象都是Iterator类型，它们表示一个惰性计算的序列
    - 函数包括lambda对变量的捕获是非即时的
    - 偏函数int2 = functools.partial(int, base=2)
9. class
    - python是一门动态语言，而且变量可以随时绑定成员变量
    - 也可以通过以下函数来访问成员变量has/get/set/del + attr()
    - 类名可以直接当变量使用，其类型为type
    - python可以多继承
    - 方法外定义的变量是类变量，同名实例变量缺失时，get会使用类变量
    - 类方法要在方法前加@staticmethod, @classmethod
    - 方法要用self作为第一个参数，但self不是关键字
    - __init__, __del__
    - override不需要修饰符
    - 内置方法，部分可当作类方法：__dict__, __doc__, __name__, __module__, __bases__
    - 其它方法：__add__, __mul__, __cmp__, __str__, __iter__, __next__, __getitem__, __setitem__, __delitem__, __getattr__, __setattr__, __call__(callable), __lt__, __eq__, __len__, __contains__, __enter__, __exit__
    - super
    - _abc: protected, __abc: private, __abc__: reserved
    - isinstance, issubclass
    - __slots__ = ()限定可扩展的实例变量名，子类的__slots__是子类与父类的和，但若子类中__slots__无则忽略父类中的__slots__
    - @property getter, @score.setter setter
    - type & metaclass
9. import
    - import先搜索当前目录，再搜索PYTHONPATH，最后搜索默念路径/usr/local/lib/python/
    - dir(): 模块中定义的模块，变量和函数
    - globals(), locals(), reload(module_name)
    - package要包含文件__init__.py
9. file & dir
    - os.rename, os.remove, os.mkdir, os.chdir, os.rmdir
9. exception
    - try except else finally
    - raise
9. enum
    - Month = Enum('Month',)
    - value默认从1算起
    - @unique可保证唯一性
    - class Gender(Enum):
        Male = 0
        Female = 1
10. pickle & jason
11. concurrency
    - Process, Pipe, Queue, Event, Semapha
    - threading, threading.local()
    - 由于GIL的存在，多线程就相当于单线程
12. coroutine
    - yield & send
    - @asyncio.coroutine(async), yield from(await), asyncio.sleep, asyncio.wait
    - 对于asyncio来说，generator就是coroutine
    - coroutine的两种调用方式：一是在另一个coroutine中被await调用，二是封装成future后加入loop
    - coroutine在被ensure_future封装的时候就指定了loop
    - 主线程默认开启loop，子线程需要手动设置loop

```python
    class ListMetaclass(type):
        def __new__(cls, name, bases, attrs):
            attrs['add'] = lambda self, value: self.append(value)
            return type.__new__(cls, name, bases, attrs)

    class MyList(list, metaclass=ListMetaclass):
        pass
```
```
    os.name
    os.uname()
    os.environ
    os.path.abspath('.')
    os.path.join('/Users/michael', 'testdir')
    os.path.split('/Users/michael/testdir/file.txt')
    os.path.splitext('/path/to/file.txt')
    copyfile()#shutil
```