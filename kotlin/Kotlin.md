## Kotlin



### 变量（variables）



*`val`* 定义常量

```kotlin
val a: Int = 1

val b = 2

val c: Int
c = 3
```



*`var`* 定义变量



**模板变量** （template）



```kotlin
val a = 1
val str = "a is $a"
```



### 条件（condition）

*`if`*

*条件赋值*



```kotlin
val a = 1
val b = 2
val max = if (a > b) a else b
```



*`when`* -> `switch`



```kotlin
when (x) {
    1 -> print("x == 1")
    2 -> print("x == 2")
    else -> { // Note the block
        print("x is neither 1 nor 2")
    }
}
```



```kotlin
when (x) {
    0, 1 -> print("x == 0 or x == 1")
    else -> print("otherwise")
}
```



```kotlin
when (x) {
    in 1..10 -> print("x is in the range")
    in validNumbers -> print("x is valid")
    !in 10..20 -> print("x is outside the range")
    else -> print("none of the above")
}

```



```kotlin
fun hasPrefix(x: Any) = when(x) {
    is String -> x.startsWith("prefix")
    else -> false
}
```



```kotlin
when{
	1 -> 
    2 -> 
}
```



*`for`*

```kotlin
for(item: String in items) {

}
```



*while*



```kotlin
while(x > 0) {

}
```



```kotlin
do {
  // TODO
} while(true)
```



### range



`in`

`!in`

`step`

`downTo`

```kotlin
for (x in 1..10 step 2) {
    print(x)
}
println()
for (x in 9 downTo 0 step 3) {
    print(x)
}
```



### Method



### 类 class

```kotlin
class A {...}
class A
class A constructor(arg: String) { ... }
class A(arg: String) { ... }
class Person(name: String) {
    init { // 初始化代码块
        
    }
}
```



*继承*

```kotlin
open class Base(p: Int)

class Derived(p: Int) : Base(p)
```

```kotlin
class MyView : View {
    constructor(ctx: Context) : super(ctx)

    constructor(ctx: Context, attrs: AttributeSet) : super(ctx, attrs)
}
```

重载方法/属性需要open

*overriding methods*

```kotlin
open class Base {
    open fun v() { ... }
    fun nv() { ... }
}
class Derived() : Base() {
    override fun v() { ... }
}
```

*overriding properties*

```kotlin
open class Foo {
    open val x: Int get() { ... }
}

class Bar1 : Foo() {
    override val x: Int = ...
}
```

```kotlin
interface Foo {
    val count: Int
}

class Bar1(override val count: Int) : Foo

class Bar2 : Foo {
    override var count: Int = 0
}
```

`super`

*super.f*

```kotlin
open class Foo {
    open fun f() { println("Foo.f()") }
    open val x: Int get() = 1
}

class Bar : Foo() {
    override fun f() { 
        super.f()
        println("Bar.f()") 
    }
    
    override val x: Int get() = super.x + 1
}
```

*super@Class.f 内部类* 

```kotlin
class Bar : Foo() {
    override fun f() { /* ... */ }
    override val x: Int get() = 0
    
    inner class Baz {
        fun g() {
            super@Bar.f() // Calls Foo's implementation of f()
            println(super@Bar.x) // Uses Foo's implementation of x's getter
        }
    }
}
```

```kotlin
open class A {
    open fun f() { print("A") }
    fun a() { print("a") }
}

interface B {
    fun f() { print("B") } // interface members are 'open' by default
    fun b() { print("b") }
}

class C() : A(), B {
    // The compiler requires f() to be overridden:
    override fun f() {
        super<A>.f() // call to A.f()
        super<B>.f() // call to B.f()
    }
}
```

*抽象类*

```kotlin
open class Base {
    open fun f() {}
}

abstract class Derived : Base() {
    override abstract fun f()
}
```

`getter/setter`

```kotlin
var <propertyName>[: <PropertyType>] [= <property_initializer>]
    [<getter>]
    [<setter>]
```

```kotlin
var stringRepresentation: String
    get() = this.toString()
    set(value) {
        field = value
    }
```



### 对象

```kotlin
val a = A()
```



`!!.` or `?.`



`!!.` 属性为空 throw Null point exception

`?.` 返回null