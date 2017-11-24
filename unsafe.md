### Unsafe Area in Swift
1. summary   
 
 |c|swift|
 |:-:|:-:|
 |const T*|UnsafePointer<T>|
 |const void*|UnsafeRawPointer|
 |T*|UnsafeMutablePointer<T>|
 |void*|UnsafeMutableRawPointer|
 |T`*` const`*`|UnsafeBufferPointer<T>|
 |T**|UnsafeMutableBufferPointer<T>|
 |T**|AutoreleasingUnsafeMutablePointer<T?> == inout|

1. malloc & free  
```c
    int *ptr = (int*)malloc(1);
    *ptr = 1;
    printf("%i", *ptr);
    free(ptr);
```
```swift
    var ptr = UnsafeMutablePointer<Int>.allocate(capacity:1)
    ptr.pointee = 1
    print(ptr.pointee)
    ptr.deallocate(capacity: 1)
```
2. existing value  
    - `&` is only available as para in Swift  
```c
    int a = 2;
    int *ptr = &a;
    *ptr = 1;
    printf("%i", a);
```
```swift
    var a = 2
    withUnsafeMutablePointer(to: &a){$0.pointee = 1}
    print(a)
```
2. read & write
```c
    int *ptr = (int*)malloc(1);
    memset(ptr, 1, 1);
    printf("%i", *ptr);
    *ptr = 2;
    printf("%i", *ptr);
    ptr[0] = 3;
    printf("%i", ptr[0]);
    free(ptr);
```
```swift
    let ptr = UnsafeMutablePointer<Int>.allocate(capacity:1)
        ptr.initialize(to: 1)
        print(ptr.pointee)
        ptr.pointee = 2
        print(ptr.pointee)
        ptr[0] = 3
        print(ptr[0])
        ptr.deallocate(capacity: 1)
```
3. cast with the same alignment
    - Int/UInt, Int8/Void...
```c
    int a = -1;
    uint *ptr = (uint*)&a;
    printf("%i", *ptr);
```
```swift
    var a = -1
    withUnsafeMutablePointer(to: &a){
                    var ptr = unsafeBitCast($0, to: UnsafePointer<UInt>.self)
                    print(ptr.pointee)
                }           
```
4. cast with different alignments
```c
    int a = 0x01020304;
    uint8_t *ptr = (uint8_t*)&a;
    printf("%i", *ptr);
    printf("%i", *(ptr + 1));
```
```swift
    var a = 0x01020304
    withUnsafePointer(to: &a){
                    $0.withMemoryRebound(to: UInt8.self, capacity: 4){
                        print($0.pointee)
                        print(($0 + 1).pointee)
                    }
                }         
```
5. cast with const
```c
    int a = 1;
    int *ptr1 = (int*)&a;
    const void* ptr2 = (const void*)ptr1;
```
```swift
    var a = 1
    withUnsafePointer(to: &a){
            let b = UnsafeMutablePointer<Int>.init(mutating: $0)
            let c = UnsafePointer<Int>.init(b)//
        }
```
5. array
    - beside functions array has methods to access its pointer
    - **BufferPointer are additional convenient methods to array, which comply with Collection protocol. They can't be created by alloc