swift-block
1.swift中block和func表现类似，这与OC不同.
(1)可以在func中定义另一个func
(2)可以互相赋值

OC:
int add(int a, int b){return a+b;}
…
int(^add1)(int) = add	//error
print(add1(3,4))

swift:
func add(a:Int,b:Int)->Int{return a+b}
…
let add1 = add
print(add1(3,4))	//7

(3)method与function互通

3.逃逸特性，@escaping表示函数返回时block不一定执行完毕
4.格式发生变化，类型和实现放在一个{}中，且用in隔开。如果类型被省略了，就不能用in了
5.block增加语法糖特性，用于不同程度的缩写
不缩写代码
let add:((Int,Int)->Int) = {(a: Int, b:Int) -> Int in
        let result = a+b
        return result}
        print(add(4,3))
(1)类型确定的情况下，类型中的参数类型，参数和返回类型可以省略，另外()本身也可以跟着参数类型一起省略
(a: Int, b:Int)
(a, b) -> Int
a, b -> Int
(a, b)
a, b
以及全部省略
为方便记忆省略全部参数，使用匿名参数

4.0新特性：语义分析时，参数优先识别为一个tuple
匿名参数可以这样访问
["a":1, "b":2].forEach {
            print("\($0.0)")
        }
["a":1, "b":2].forEach {
            print("\($0.key)”)
        }

(2)单条语句可以省略return
let add:((Int,Int)->Int) = {(a: Int, b:Int) -> Int in
        a+b}
        print(add(4,3))
(3)自动命名的参数$0,$1...
let add:((Int,Int)->Int) = {$0+$1}
        print(add(4,3))
(4)后置
作为最后一个参数时可以移到()外面
出现if在表达式中除外
(5)作为唯一一个参数时可以省略()
block作为函数唯一参数时，函数本身的()也可以省略
func setFun(fun:(Int)->Int)->Int{
            return fun(4)
        }
print(setFun{$0*3})

(6)如果有参数则要至少处理一个。
{a in}
{_ in}

6.如果语句复杂，block类型不可省略

7. 自动闭包
@autoclosure 可以省略{}把仅有的一句表达式变成func
8.引用类型
“[weak self, (unowned self, )weak delegate = self.delegate!]” before Params or in
Convention (block/swift/c)

