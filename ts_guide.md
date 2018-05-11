### Outline
1. 基础类型
    - string，boolean，number，Array，枚举，Any， Never，cast
    1. ``可跨行，替换格式为${}
    2. tuple的形式与应用都和数组类似
    3. tuple的元素类型是已知元素类型的联合
    3. 类型void，null，undefined，前者可以被后两个赋值，后两个存在同名实例，后两者是所有类的子类
    3. 非const枚举被反射
    4. any不作属性和方法检查，Object会
    5. cast用<string>或as
2. 变量声明
    - 解构，默认值，展开
    1. var，let，const
    1. =>会capture，即使用的是数值，而普通方法不会capture，即使用的是引用
    2. 可用【】解构数组和tuple，用{}解构对象，也可以对属性重命名
    3. 解构类型可以是类型，也可以是数值
    4. 解构标签中的默认值为标签的默认值，类型中的默认值为整个参数的默认值
    5. 展开可以覆盖，可以做浅copy
    6. 展开对象会丢失方法
3. 接口
    - 可选属性，只读属性，属性类型
    1. 比较时函数及方法时可忽略函数标签的名称
    1. 接口只定义了一函数类型时可以描述函数
    2. 接口可以描述索引特性
    3. 接口可以描述构造器
    3. number会被转换成${number}再去索引，所以同时存在number和string索引时，number索引返回值要是string索引返回值的子类
    4. string索引返回值类型要与其它属性类型一致
    5. 继承和转换其实就是成员的copy
    6. 对象和函数可以互转
    7. 接口可以继承类，继承这样接口的类只能是原类的子类
4. 类
    - javascript使用函数和基于原型的继承来复用，而typescript使用基于类的继承来复用。因为类对象就是个构造器，所以定义类的时候生成了两个东西：实例类型和构造函数
    1. 默认权限为public
    3. super仅用作方法
    4. 不同类的实例转换：a = b，要求b有a的所有成员，a中不包含非public的成员
    5. 构造器的参数加访问权限类型后会自动生成属性
    6. 使用set和get构造访问器，只有get的属性是只读属性
    7. 抽象类可实现函数，抽象方法只存在于抽象类
    8. 类可以当接口使用
5. 函数
    1. 函数实现时，返回类型可以被推导，所以不需要注明返回类型
    2. 捕获变量是函数的隐藏状态，不属于api
    3. 可选参数与末尾的默认参数共享函数类型
    4. 捕获this的函数需要假参数把类型从any转换成具体类型，这与swift中方法转函数的道理一样
    5. =>会捕获this的数值，但不会捕获this的类型
    6. 重载需要一个总的入口函数来处理所有同名函数
6. 范型
    1. 范型可描述函数，接口，类，构造函数
    1. 范型不能描述静态变量
7. 枚举
    - 普通枚举，常量枚举，外部枚举
    1. 普通枚举是一个类，编译时会生成值到名字的双向映射
    2. 常量枚举以及没有初始化方法的普通枚举，在编译时会被替换成常量，且不含计算过程
    3. 外部枚举相当于extern，且不会被替换成常量
8. 类型推导
    - 推导分为最佳推导和上下文推导，其实质是两两比对
    1. 若没有找到数组及tuple的已出现的通用类型，则类型是是所有元素类型的和。所以没有出现的共同基类会被忽略
    2. 上下文相关推导发生在函数传递参数，赋值两边，类型转换，对象成员和数组字面量，返回语句
9. 类型兼容
    - typescript有两种兼容类型：子类型和赋值兼容，后者扩展了前者。赋值兼容的对象类，枚举，接口，函数，使用的原则是结构类型，即是否兼容是由其成员决定的，不像其它大部分语言使用的是名义类型，即是否兼容由自身名称决定的。其实质是运行时是否可以忽略多余的成员，因为类成员会自动初始化，所以类的兼容是退化的，因为函数参数不会自动初始化，所以函数的兼容是进化的
    1. 兼容性检查是递归的
    2. 枚举与数字是兼容的，但不同枚举不兼容
    3. 类的静态变量不参与比较
    4. 范型自身不参与比较
    5. 重载的函数要比较每一个具体的实现
    6. 可选参数及剩余参数，比较函数兼容性的时候，可选参数与必须参数是可互换的。 源类型上有额外的可选参数不是错误，目标类型的可选参数在源类型里没有对应的参数也不是错误。
10. 高级类型
    1. 当一个函数有剩余参数时，它被当做无限个可选参数
    2. 交叉（&）的结果拥有元素的所有成员
    3. 联合（|）的结果拥有元素的共同成员
    4. 自定义类型保护作用于函数：parameterName is Type
    5. typeof类型保护：typeof v === "typename"
    6. instanceof类型保护：v instanceof Type
    7. 设置strictNullChecks后，type | null不支持undefined，而可选参数和属性则不接受null
    8. type | null的拆包value || default及value！
    9. 别名在编译时被替换成原型
    10. 别名出现在右边时仅限于属性
    11. 别名不能被extends和implements
    12. typescript支持常量类型，且相同常量类型可以交叉和联合
    13. keyof T相当于string(|string)*
    14. T[K]会自动判断返回类型，如果T可以有type类型的索引，那么T[K]的类型是type，且T[k]就是type
11. 映射
    - 映射是根据旧类型创建新类型，一般会改变成员属性
    
???
    1. type, type, value, :, =
```typescript
    type Readonly<T> = {readonly [P in keyof T]: T[P];}
    type DeepReadonly<T> = {readonly [P in keyof T]: DeepReadonly<T[P]>;}
    type Partial<T> = {[P in keyof T]?: T[P];}
    type Nullable<T> = { [P in keyof T]: T[P] | null }
    type Pick<T, K extends keyof T> = {[P in K]: T[P];}
    type Record<K extends string, T> = {[P in K]: T;}
```
```typescript
    function getProperty<T, K extends keyof T>(o: T, name: K): T[K] {
    return o[name]; // o[name] is of type T[K]

    type Keys = 'option1' | 'option2';
    type Flags = { [K in Keys]: boolean }; 
}
```
```typescript
    class Control {
        private state: any;
    }

    interface SelectableControl extends Control {
        select(): void;
    }

    class Button extends Control implements SelectableControl {
        select() { }
    }

    class TextBox extends Control {

    }

    // 错误：“Image”类型缺少“state”属性。
    class Image implements SelectableControl {
        select() { }
    }
```

```typescript
    interface Counter {
        (start: number): string;
        interval: number;
        reset(): void;
    }

    function getCounter(): Counter {
        let counter = <Counter>function (start: number) { };
        counter.interval = 123;
        counter.reset = function () { };
        return counter;
    }

    let c = getCounter();
    c(10);
    c.reset();
    c.interval = 5.0;
```
```typescript
    interface ClockConstructor {
    new (hour: number, minute: number): ClockInterface;
    }
    interface ClockInterface {
        tick();
    }

    function createClock(ctor: ClockConstructor, hour: number, minute: number): ClockInterface {
        return new ctor(hour, minute);
    }

    class DigitalClock implements ClockInterface {
        constructor(h: number, m: number) { }
        tick() {
            console.log("beep beep");
        }
    }
    class AnalogClock implements ClockInterface {
        constructor(h: number, m: number) { }
        tick() {
            console.log("tick tock");
        }
    }

    let digital = createClock(DigitalClock, 12, 17);
    let analog = createClock(AnalogClock, 7, 32);
```