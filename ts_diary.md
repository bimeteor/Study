### diary
1. boolean
2. number
3. string
    - ${}
    - ``
```javascript
    let a = `
    abc"12"
    `
```
4. array
    - number[]
    - Array<number>
    - ReadonlyArray<number>
```javascript
    let a = [1,2,3]
    let b:ReadonlyArray<number> = a
    a = b//error
    a = b as number[]

    function f([first, second]: [number, number]) {
        console.log(first);
        console.log(second);
    }
    f(input);
```
5. tuple
    - []
    - [n] -> type(|type)*
    - (type(|type)*)[]
6. enum
    - string
    - Type[n]
    - Enum[Enum.A]
    - const enum Enum
    - declare enum Enum
    - 映射和内联
7. any
    - vs Object:compile check
8. empty
    - void/undefined/null
    - --strictNullChecks
9. never
    - unreachable
10. cast
    - (<string>someValue).length
    - (someValue as string).length
11. array
    - let arr = [1, 2]; let [first, second] = arr; //arr.first
    - let [first] = [1, 2]
    - let [first, ...rest] = [1, 2, 3, 4]
    - let [, second, , fourth] = [1, 2, 3, 4]
12. class
    - vs tuple: label
    - let {a, b} = {m:"foo", n:12}
    - let {m, n} = {m:"foo", n:12}
    - let { a: newName1, b: newName2 } = o
    - constructor(private name: string)
    - readonly
    - get/set
    - super can operate functions only
    - let obj = {["sym"]:"aa"}
    - 对象的字面量会进行参数检查，包括？
13. type
    - type T = number
14. default
15. interface
    - option:?
    - readonly
    - check paras & return types automatically
    - index & KVC
```javascript
    interface LabelledValue {
        label: string;

    }
    function printLabel(labelledObj: LabelledValue)...
    let obj = <LabelledValue>{}
```
16. literal additonal check
    - it fails if unnessarry variable exists
    - casting makes it doesn't happen
17. abstract
19. extends
```typescript
    class Point {
    x: number;
    y: number;
}
interface Point3d extends Point {
    z: number;
}

let point3d: Point3d = {x: 1, y: 2, z: 3};
```
20. function
    - return type：实现可以为空，类型不能为空
    - optional:
    - default:no input or null input
    - optioanl & default are the same type
    - rest
    - this as first para
    - lamda captures paras
    - overload:any
    - 申明和实现不一样，申明和lamda一样
    - 
```typescript
    let ff:()=>void = function(){}
    let f:{():void} = ()=>{}
```
21. generic
    - 静态属性不能使用这个泛型类型
```typescript
    interface Empty<T> {
    }
    let x: Empty<number>;
    let y: Empty<string>;

    x = y;
```
```typescript
    interface NotEmpty<T> {
        data: T;
    }
    let x: NotEmpty<number>;
    let y: NotEmpty<string>;

    x = y;  // error, x and y are not compatible
```
```typescript
    function identity<T>(arg: T): T {
        return arg;
    }
    let myIdentity: <U>(arg: U) => U = identity;
    let myIdentity: {<T>(arg: T): T} = identity;
```
22. &|
    - function(x:type):x is aType
    - typeof padding === "number"
    - obj instanceof constructor
23. alias
    - type Container<T> = { value: T };
    - 除了修饰属性外，别名不能出现在声明语句右边
    - 类型别名不能被extends和implements（自己也不能extends和implements其它类型）
    - type Easing = "ease-in" | "ease-out" | "ease-in-out";

```typescript
    type Tree = {
        node:Tree
    }

    function createElement(tagName: "img"): HTMLImageElement;
    function createElement(tagName: "input"): HTMLInputElement;
    // ... more overloads ...
    function createElement(tagName: string): Element {
        // ... code goes here ...
    }

    interface Square {
        kind: "square";
        size: number;
    }
    interface Rectangle {
        kind: "rectangle";
        width: number;
        height: number;
    }
    interface Circle {
        kind: "circle";
        radius: number;
    }
    type Shape = Square | Rectangle | Circle
    function area(s: Shape) {
    switch (s.kind) {
        case "square": return s.size * s.size;
        case "rectangle": return s.height * s.width;
        case "circle": return Math.PI * s.radius ** 2;
    }
}
```
24. symbol
    - symbol("a") !== symbol("a")
```typescript
    const getClassNameSymbol = Symbol();

    class C {
        [getClassNameSymbol](){
        return "C";
        }
    }

    let c = new C();
    let className = c[getClassNameSymbol](); // "C"
```
25. expand
    - 可用于浅copy
    - 展开对象会丢失方法
```typescript
    let first = [1, 2];
    let second = [3, 4];
    let bothPlus = [0, ...first, ...second, 5];

    let defaults = { food: "spicy", price: "$$", ambiance: "noisy" };
    let search = { ...defaults, food: "rich" };
```
26. 解构
    - []：解构数组，tuple，可省略，可。。。
    - {a：type，b:type}：解构对象，标签名要一致。标签后可带？
    - 解构可用于函数参数，其类型可以是数组，tuple，对象类型，也可以是具体数值
    - 标签中的默认值为标签的默认值，类型中的默认值为整个参数的默认值
```typescript

```

```typescript
    function keepWholeObject(wholeObject: {a: string, b?: number}) {
        let {a, b = 1001} = wholeObject;
    }
    function f({a, b}: C)...
    function f({a, b = 0} = {a: ""}): void {
        // ...
    }
    f({a: "yes"}) // ok, default b = 0
    f() // ok, default to {a: ""}, which then defaults b = 0
    f({}) // error, 'a' is required if you supply an argument
```
