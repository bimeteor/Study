1. 基础
    - 多行语句用\，但[], {} 或 () 之间的内容就不需要\
    - 用 '，"，'''，"""表示字符串，其中后两个可以跨行
    - expr与stmt之间用 :隔开
    - 第一行指定解析器：#!/usr/bin/python和#!/usr/bin/env python
2. 变量
    - 标准类型：int, long, float, complex, str, list, dict, tuple
    - a, b, c = 1, 2, "john"
    - del a, b, c
    - 下标：[start, end, interval], 不包括上界，上下界可省，可双向，下界较小时，间隔要负，否则要正
    - range(start, end, interval)参数意义和下标一致
    - 对于str，*是重复操作
    - 类型转换为行为式
    - tuple不能更新
    - 用，隔开的对象默认为tuple
    - (), (1,)
3. 运算符
    - **为幂值
    - //为商的整数部分
    - and，or，not，in，not in，is，is not
    - id(o), 整数会复用内存
8. str
    - r/R'abc'：去转义
    - 'abc'%tuple
8. dict
    - key可以是numbers， str， tuple，及自定义的对象
    - dict['a']不存在的话会抛出异常
    - del dict['a'], dict.clear()
9. 类
    - python是一门动态语言，而且变量可以随时绑定成员变量
    - 也可以通过以下函数来访问成员变量has/get/set/del + attr()
    - 类名可以直接当变量使用，其类型为type
    - python可以多继承
    - 方法要用self作为第一个参数，但self不是关键字
    - __init__, __del__
    - override不需要修饰符
    - 内置方法，部分可当作类方法：__dict__, __doc__, __name__, __module__, __bases__
    - 其它方法：__add__, __cmp__, __str__
    - super
    - _abc: protected, __abc: private, __abc__: reserved
    - isinstance, issubclass


