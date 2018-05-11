1. 基本知识
    1. 与swift相比，val，var相当于let，var
    2. const val表示编译期常量，其expr中的变量仅限于const val常量
    12. 与swift相比，Uint相当于Void，可省略，Nothing相当于Never
    4. 未使用的参数可用`_`代替，但是`_`不能用var和val声明
    3. 与swift一致，整形数字间可用`_`连接
    13. Kotlin没有Scalar类型，一切皆是类，根类型为Any
    10. 与swift不同，类型判断具有上下文相关性
    6. 类型别名typealias State = Int
3. String
    1. String不可变
    2. "$name"/"${expr}"
    5. 与swift一致，"""abc"""
    6. 字符：'a'，不能和数字直接运算
    8. 语句变表达式：if，when和try
2. 位操作
    shl(bits) –>  <<
    shr(bits) –>  >>
    ushr(bits) –>  >>>
    and(bits) –> &
    or(bits) –> |
    xor(bits) –> 
    inv() –> ~ 
2. null 
    1. 与swift相比，`?` = `?`, `!!` = `!`, `?:` = `??`，
    2. 与swift相比，null使用较为宽松，null支持更多方法
    3. 与swift相比，null使用更为方便，因为判断对下文有效
    4. 与swift相比，??仅支持expr，而?:支持expr和stmt
    5. 与swift相比，optional chain语句中，swift只需要在返回值为optional的语句后加？，而kotlin则需要从nullable的第一个语句开始全部加？
    6. 与swift相比，subcribe语法糖col?[i]不可用，只能老老实实用get(i)？
    5. 常用代码：
        1. if (obj != null) stmt -> obj?.let{stmt}
        2. if (obj == null) stmt -> obj?:stmt
        3. if (obj != null) stmtif else stmtelse -> obj?.let{stmtif} ?: stmtelse
4. collections
    1. (MutableList<E>:List<E>|MutableSet<E>):Set<E>:Collection<E>:Interable<E>
    2. HashSet<E>|TreeSet<E>-AbstractSet<E>~AbstractCollection<E>~Collection<E>:
    3. SortedSet<E>:Set<E>
    4. LinkedHashSet<E>-HashSet<E>~
    5. Array<E>
    6. Hashtable<K, V>-Dictionary<K, V>~Map<K,V>:
    7. LinkedHashMap<K, V>-HashMap<K, V>-AbstractMap<K,V>~Map<K,V>:
    2. (Mutable)(List|Set|Map)均是interface，类实现为ArrayList，HashSet，SortedSet，TreeSet，HashTable，HashMap，TreeMap
    6. Sequence可用于未知长度，相当于python的generator
    3. 判断Set中元素是否同等的方法是hashCode()和equals()
    1. 与大多语言不一样，没有Array literal
    2. (((int|byte|...)A)|a)rrayOf((e(,e)*)?)
    3. Array(n, {i->o})
    4. for ((index, value) in array.withIndex())
    5. functions
        1. any = contains，all，count, none
        7. fold = reduce, foldRight
        8. reduce无初值，reduceRight
        8. forEach = forEach
        8. forEachIndexed = indices.forEach
        9. maxBy = max, minBy = min
        10. sumBy
        11. drop = drop，dropLast = dropLast，dropWhile，dropLastWhile
        12. filter = filter，filterNot，filterNotNull
        13. slice无operator[]，但slice可以是Range或List
        14. take前n个，takeLast，takeWhile，takeLastWhile
        15. flatMap先生成集合的集合，再合并集合，无去null功能
        16. groupBy，partition
        17. map = map
        18. mapIndexed，mapNotNull
        19. contains = contains
        20. elementAt
        21. elementAtOrElse，elementAtOrNull
        22. first = first，firstOrNull
        23. indexOf
        24. indexOfFirst，indexOfLast
        25. last，lastIndexOf，lastOrNull
        26. single，singleOrNull
        27. 【merge】
        28. plus = +
        29. zip
        30. reversed
        30. sort = sorted = sortBy，sortDescending，sortDescendingBy
5. when
    1. when((x))?{...else}代替switch(x){...default}，else代替default。expr->{}，expr如果包含x，则expr是x的普通枚举，is或in表达式；否则，expr只要是bool表达式即可
    2. when可变表达式
3. cast
    1. is和!is判断类型，且对下文有效
    3. as和as?，仅子类可向父类转换
4. range
    - range:: rangeTo|downTo|until(step n)?
    rangeTo:: low..high, 
    downTo:: high downTo low,
    until:: low until high,
    [low, high]:: [Char, Char]
                |[(Byte|Short|Int|Long|Float|Double), (Byte|Short|Int|Long|Float|Double)]
                |[String, String]
2. fun
    1. 返回类型可省，public除外，但若返回类型是Unit，public类型也可省
    2. 如果函数体只有一个expr，则可以 = expr
    3. 可变参数前加vararg
    4. 参数可提供默认值
    5. 函数调用时可提供参数名
    4. 函数引用::name
    5. inline的实质是代码替换
    6. 符号化函数需要operator修饰
4. lambda
    1. 与swift相比，lambda和普通函数在形式上没有区别。
    2. 与swift相比，缩写方式相同的是，作为最后参数时可以外置，作为唯一参数时可以去（）
    2. 与swift相比，缩写方式不同的是，只有一个参数时参数才可省略，默认名称为it
    3. 与swift相比，作为inline函数的参数时，return默认返回至外层函数
5. 标签及跳转
    1. 标签格式：name@ expr|stmt，lambda的标签在{}前面
    2. 标签搭配break，continue，return使用，其中return@name (res)?，仅return可跨越ladmbda的范围
    3. 函数包括ladmbda的默认标签为函数名
5. class
    1. 允许空类
    2. 一主构造器，多次构造器
    3. 主构造器紧跟类名，且没有权限修饰时constructor可省略
    4. 主构造器不含代码，初始化可在init中进行
    4. 系统会提供一个默认的无参主构造器，人为提供的主或次构造器会让默认构造器失效
    4. 人为提供主构造器后，次构造器必须直接或间接调用主构造器，调用方式为constructor(...):this(...)
    4. 可在主构造器参数前加val，var来声明成员变量
    4. 成员权限种类与类权限一样，默认为public
    4. getter权限要与成员变量相同，setter权限要与成员变量相同或更低
    5. 非空属性要在类初始化时赋值，可用lateinit改变这一限制
    12. lateinit要求：
        - 用var声明且不在主构造函数中
        - 没有自定义setter或getter
        - 非原始类型且非null
    5. 重写setter或者显式调用访问field时，Backing Fields生效
    5. override用来重载成员方法和变量，可出现在constructor中，可val->var，反之则不可
    11. 静态成员只能通过嵌套object类或者搭配companion类实现
    6. 抽象类和方法
    7. 嵌套类不可访问外部类成员
    8. 内部类用inner修饰，可以直接访问外部类成员，可用this@className获取外部对象
    9. Any含有3个方法
        - equals()
        - hashCode()
        - toString()
    10. 类和权限修饰符
        - classModifier: 类属性修饰符，标示类本身特性。
            - abstract    // 抽象类  
            - final       // 类不可继承，默认属性
            - open        // 类可继承
            - enum        // 枚举类，无普通枚举类型
            - annotation  // 注解类
        - accessModifier: 访问权限修饰符
            - private    // 仅在同一个文件中可见
            - protected  // 同一个文件中或子类可见
            - internal   // 同一个模块中可见
            - public     // 所有调用的地方都可见，默认属性
9. enum class
    - Kotlin无通常意义的枚举，取而代之的是枚举类
    - 枚举类的实质是有限的类实例
    - 枚举类可有enumValues<T>() 和 enumValueOf<T>(str:String)进行映射
    - 枚举实例有两属性val name: String和val ordinal: Int
    - 枚举数值默认从0开始，可增加constructor参数改变默认数值，但只有增加属性变量才可访问其数值
10. data class
    - 数据类的限制：
        1. 主构造器至少有一个属性参数，且所有参数均含属性
        2. 类不能被修饰为abstract, open, sealed 或者 inner
        3. 不能继承其它类
    - 自动实现的方法，仅对主构造器中的参数有效
        1. equals(),hashCode()
        2. toString() //"User(name=John, age=42)"
        3. componentN() //functions
        4. copy()
    - 解构: val (name, age) = User(name = "", age = 2)
    - 标准数据类：Pair/Triple
11. sealed class
    - 有效的子类
    - 不能修饰interface, abstract
13. object
    - 把类声明变成expr，可增加类成员和override，且所有成员均为静态类型
    - object表达式可省略类型变匿名类
    - 用object声明的类，所有成员均为静态类型
14. companion
    - companion用来给类增加静态成员，且一个类只能使用一次
    - companion类可匿名，匿名时名称可用Companion，但无论是否匿名，外部类都可直接访问其成员
8. extension
    - 扩展是静态的
    - 扩展函数优先级较低
    - 扩展成员变量时field不可用
    - 嵌套扩展时，可以直接访问外部类的成员，若有相同成员则以嵌套类优先
    - 扩展空对象Any?.fun()时可用this判断对象是否为空
    - 扩展一般放在顶级包下，导入扩展: import (foo.bar.goo|*)
    - 常用扩展方法：
        - `TODO(String?) vs //TODO:frank`
        - [swift]`fun <T, R> T.let(block: (T) -> R): R`相当于Optional.map
        - let, if-else, return优先使用let的因素：对新生成对象进行判断时，方法体中仅含一两个expr|stmt, 无return或搭配label可轻松return
        - let中block返回值类型是由最后一个stmt决定的。如果stmt为expr，则返回类型与expr一致，否则为Unit
        - 赋值空+返回：`val type = node.getAttribute("type") ?: return ""`
7. interface
    1. 相swift不同的是，interface中可以定义抽象成员变量，可以实现方法
12. generic
    - 泛型约束，默认的上界是 Any?
    - 多个上界约束条件，可以用 where 子句：where T：Comparable, Cloneable
    - in和out分别限制泛型用于成员变量和方法时的数据流向
    - *表示不关注其类型，主要用于从java转换过来的类型，如List<*>, Map<*, Int>
15. by
    - 可委托对象，属性，方法
    - 委托的实质是编译器自动加入私有变量和方法
    - 搭配map实现自身属性的委托
    - 搭配lazy实现惰性加载，对象可以是成员变量和变量自身
    - 搭配lazy(block), block.isValid()实现block的惰性加载
    - 搭配Delegates实现观察模式，观察对象可以是成员变量，可以是变量自身
    - 搭配Delegates.notNull解决对象初始化时不能给成员变量赋值的问题
16. thread
    - 创建thread的两种方法：object expr和block
    - 同步方法@Synchronized，同步块synchronized(Lock)
    - 变量安全@Volatileannotation
11. coroutine
    - 协程的特点是无阻塞更廉价可控，会为每个挂起的函数生成一个Continuation对象保存状态和局部变量
    - 协程与线程的区别
        1. 线程通过操作系统调度CPU来实现，协程通过编译器插入代码实现
        2. 线程切换代价高，需要切换上下文，协程几乎无代价
        3. 线程阻塞代价高，尤其是高负载情况下，协程不会发生阻塞
        4. 线程挂起是随机的，协程只能在指定位置挂起
        5. 线程的行为需要切换内核空间的参与，而协程的行为完全发生在用户空间
        6. 线程是抢占式的，而协程是非抢占式的，所以需要手动切换
        7. 线程是被分割的CPU资源, 协程是组织好的代码流程，线程本身也是协程的资源



？？
lock & block

```kotlin
    private val lock = java.lang.Object()

    fun produce() = synchronized(lock) {  
    while (items >= maxItems) {
        lock.wait()
    }
    Thread.sleep(rand.nextInt(100).toLong())
    items++
    println("Produced, count is $items: ${Thread.currentThread()}")
    lock.notifyAll()
    }

    fun consume() = synchronized(lock) {  
    while (items <= 0) {
        lock.wait()
    }
    Thread.sleep(rand.nextInt(100).toLong())
    items--
    println("Consumed, count is $items: ${Thread.currentThread()}")
    lock.notifyAll()
    }
```