### Outline
1. 基础类型
    - string，boolean，number，Array，枚举，Any， Never，cast
    1. ``可跨行，替换格式为${}，支持tagged template
    2. tuple的形式与应用都和数组类似，只不过元素类型是已知元素类型的联合
    3. 类型void，null，undefined，前者可以被后两个赋值，后两个存在同名实例，后两者是所有类的子类
    3. 非const枚举被反射
    4. any不作属性和方法检查，Object会
    5. cast用<string>或as，只会改变读写属性
    6. 用{}手动创建对象时key:value中的key可以是string literal，可以省略为key，如果key不是name，需要放在[]里面
2. 变量声明
    - 解构，默认值，展开
    1. var，let，const
    1. =>会capture，即使用的是数值，而普通方法不会capture，即使用的是引用
    2. 可用[]解构数组和tuple，用{}解构对象，也可以对属性重命名。[]可以放在参数列表使用
    3. 解构类型可以是类型，也可以是数值，解构可以嵌套
    4. string可以被destruct成sequence
    4. 解构标签中的默认值为标签的默认值，类型中的默认值为整个参数的默认值
    5. 后面元素会覆盖前面元素
    6. 展开对象会丢失方法
    7. destruct用于交换数值
3. 集合
    7. ...可以用在参数列表和[]中，场景有把array转成可变参数，copy，合并，desctruct，以及string，Map，Set，Iterator，Generator转array
    8. Array.from把有length的对object转成array，替代方案[].slice.call(args)
    9. Array.of补充Array()，替代方案是[].slice.call(args)
    10. fill(),entries()，keys() 和 values(),includes(),flat()，flatMap(), in
    11. Map 和 Set 数据结构有一个has
    12. Set比较用的是===
    2. WeakSet元素只能是对象，而且不可遍历
3. 接口
    - 可选属性，只读属性，权限类型，可约束函数和类
    - 因为TypeScript的类型检查用的是结构型检查，所以接口的实现和类的转换可以只做成员的匹配，不做显示的实现和继承
    1. 函数签名不包括函数名，实现的时候不会比较参数名
    1. 用new约束constructor时不能用类来implements，因为constructor属于静态方法，而约束只检查实例方法
    3. 成员变量类型可以是常量
    3. number索引会被转换成string再去索引，所以同时存在number和string索引时，number类型要是string的子类。其它成员类型要是string的子类
    5. 继承和转换其实就是成员的copy
    7. 接口继承类会去掉所有的实现，继承被继承类有非public成员，只能用原类的子类来实现该接口
    8. type aType = {} literal
4. 类
    - javascript使用函数和基于原型的继承来复用，而typescript使用基于类的继承来复用。因为类对象就是个构造器，所以定义类的时候生成了两个东西：实例的类型和静态方法constructor
    1. 默认权限为public
    3. 成员变量必须赋予编译常量表达式或在constructor初始化
    4. 不同类的实例转换：b = a，要求b的成员全部对a可见
    4. 生成实例的方法有两种，用new触发constructor，或者在已有其它实例或map上手动添加成员
    5. 构造器的参数用访问权限或读写属性修饰后会自动变成成员变量
    6. 使用set和get构造访问器，只有get的属性是只读属性
    7. 抽象类可实现函数，抽象方法只存在于抽象类
    8. 类可以当接口使用
    9. Object的扩展方法
5. 函数
    1. 支持默认，可选，可变参数。其中后两者要在最后，可选参数与末尾的默认参数共享函数签名
    2. 手动构造实例时，需要使用假参提供类型
    5. =>是匿名函数，是会捕获this的数值，但不会捕获this的类型。不适用于动态场景：类方法和回调
    6. overload需要一个兼容函数负责实现
    7. name(constructor为anonymous),length
6. 范型
    1. 范型可描述函数，接口，类，构造函数，可以用接口约束
    1. 范型不能描述静态变量
    2. 约束类类型即constructor时用类型用{new():T}
7. 枚举
    - 普通枚举，常量枚举，外部枚举
    1. 枚举数值可以是number和string，默认从0开始。
    2. const枚举成员必须是编译期常量表达式
    1. 普通枚举是一个类，编译时会生成值到名字的双向映射
    3. 外部枚举相当于extern，且不会被替换成常量
    5. 枚举会在逻辑运算时检查集合完整性
9. 类型兼容
    - 赋值时发生兼容，分为类和函数兼容两种，因为类成员已初始化，所以类的兼容在成员包容上是退化的，因为函数参数需要初始化，所以函数的兼容在参数包容上是进化的。函数的兼容对顺序有要求
    1. 兼容性检查是递归的
    2. 枚举与数字是兼容的，但不同枚举不兼容
    3. 类的静态变量不参与比较
    4. 范型自身不参与比较
    5. 重载的函数要比较每一个具体的实现
    6. 判断函数兼容性的时候，不考虑可选参数和默认参数，剩余参数可当做无限个可选参数
10. 高级类型
    1. 当一个函数有
    2. 交叉（&）的结果拥有元素的所有成员
    3. 联合（|）的结果拥有元素的共同成员
    4. 类型谓词parameterName is Type的推导在if-else上下文有效
    5. typeof类型保护限于：typeof v === "typename"和typeof v !== "typename"， "typename"必须是 "number"， "string"， "boolean"或 "symbol"
    6. instanceof类型保护：v instanceof Type
    7. 设置strictNullChecks后，type | null不支持undefined，而可选参数和属性则不接受null
    8. type | null的拆包value || default及value！
    9. 类型别名不会创建新名字，在编译时被替换成原型，类型别名出现在右边时仅限于成员变量的类型。接口别名会创建新名字
    11. 别名不能被extends和implements
    12. 同内型常量（string, number, 简单Enum）及其交叉和联合可以做为类型，可用于overload
    13. 可辨识联合需要有相同属性具有不同常量类型，switch会做完整性检查
11. 映射
    - 映射是根据旧类型创建新类型，一般会改变成员属性，核心是{[P in keyof T]:T[P]}，T[k]是成员类型，keyof T相当于string(|string)*
    - K extends keyof T映射是同态的，会copy属性，否则是不同态的，会生成新的成员变量，所有不会copy属性
12. Symbols
    - 唯一标识符，强大到可当类成员变量和方法，Symbol.hasInstance等内置笔法
13. 合并
    - 若没有成员冲突声明可以合并：namespace之间，interface之间，namespace和interface，class和namespace，class和interface，除此之外，namespace还可以声明为function声明变量，为enum提供扩展
    
???
    1. type, type, value, :, =
```typescript
    type Readonly<T> = {readonly [P in keyof T]: T[P];}
    type DeepReadonly<T> = {readonly [P in keyof T]: DeepReadonly<T[P]>;}
    type Partial<T> = {[P in keyof T]?: T[P];}
    type DeepPartial<T> = {[P in keyof T]?: DeepPartial<T[P]>}
    type Nullable<T> = { [P in keyof T]: T[P] | null }
    type DeepNullable<T> = { [P in keyof T]: DeepNullable<T[P]> | null }
    type Pick<T, K extends keyof T> = {[P in K]: T[P];}
    type Record<K extends string, T> = {[P in K]: T;}
```
```typescript
    Exclude<T, U> -- 从T中剔除可以赋值给U的类型。
    Extract<T, U> -- 提取T中可以赋值给U的类型。
    NonNullable<T> -- 从T中剔除null和undefined。
    ReturnType<T> -- 获取函数返回值类型。
    InstanceType<T> -- 获取构造函数类型的实例类型。

type T00 = Exclude<"a" | "b" | "c" | "d", "a" | "c" | "f">;  // "b" | "d"
type T01 = Extract<"a" | "b" | "c" | "d", "a" | "c" | "f">;  // "a" | "c"

type T02 = Exclude<string | number | (() => void), Function>;  // string | number
type T03 = Extract<string | number | (() => void), Function>;  // () => void

type T04 = NonNullable<string | number | undefined>;  // string | number
type T05 = NonNullable<(() => string) | string[] | null | undefined>;  // (() => string) | string[]


type T10 = ReturnType<() => string>;  // string
type T11 = ReturnType<(s: string) => void>;  // void
type T12 = ReturnType<(<T>() => T)>;  // {}
type T13 = ReturnType<(<T extends U, U extends number[]>() => T)>;  // number[]
type T14 = ReturnType<typeof f1>;  // { a: number, b: string }
type T15 = ReturnType<any>;  // any
type T16 = ReturnType<never>;  // any
type T17 = ReturnType<string>;  // Error
type T18 = ReturnType<Function>;  // Error

type T20 = InstanceType<typeof C>;  // C
type T21 = InstanceType<any>;  // any
type T22 = InstanceType<never>;  // any
type T23 = InstanceType<string>;  // Error
type T24 = InstanceType<Function>;  // Error
}
```

```typescript
    setTimeout(function () {
    console.log('three');
    }, 0);

    Promise.resolve().then(function () {
    console.log('two');
    });

    console.log('one');
```