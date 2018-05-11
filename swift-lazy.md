深度Swift之lazy
大家都知道，`lazy`作为成员变量的修饰关键字时有懒加载的作用，但很少人知道，`lazy`作为集合方法的时候做的事情更多
1. 作为成员变量的修饰关键字
```swift
    class Dog{
        lazy var name = "Rony"  //bad example
        lazy var age:Int = {return 3}()
        lazy var height = (0...999).reduce(0){$0 + $1}
        lazy var weight:Float = {return 9.8}()  //bad example
        init() {
            print(weight)
        }
    }
```
非`Optional`类型的成员变量要在类初始化的时候赋值，其右值表达式要在这个时候运算完毕。而`lazy`修饰符打破了此规则，把运算和赋值推迟到该成员变量第一次使用的时候。
使用适当的`lazy`必须同时满足两个条件：
    1. 成员变量不需要立刻使用
    2. 成员变量比较耗费资源，不管是CPU是Memory
因此我们看到：
    1. `name`不适合，字符串不耗资源
    2. `weight`不适合，初始化的时候被使用

2. 作为集合的方法
```swift
    let arr:[Int] = [1,2].lazy.map{
            print($0)
            return $0 * 2
        }
        print("--------")
        let _ = arr[1]
```
运行结果：
```
    --------
    2
```
从上面的例子可以看出，`lazy`作为集合方法的时候不仅起到懒加载的作用，还能节省不必要的运算。其实质是，`lazy`方法返回`LazyCollectionProtocol`，而懒加载和节省运算是`LazyCollectionProtocol`的行为