# Essential Scala for CDP Day 3

## Companion Objects
A companion object is an object
1. with the same name as a type (class or trait declaration)
2. in the same file as the type declaration

Companion objects are usually used for (additional) constructors and utility methods (equivalent in Java is static methods).


## Reasoning About Recursion
We assume the recursion is correct, in a structural recursion, as it is given to us by the recursion rule. We don't need to try to "think through" the recursion. Just accept we have a value that is correct and think about how we combine it with the other values at this step of the recursion.


## Multiple Parameter Lists
They exist and they aren't a big deal.


## Methods Without Parameter Lists

You can define a method without any parameter list:

```scala
def noParams: Int = 42
```

You can also define a method with an empty parameter list:

```scala
def emptyParams(): Int = 42
```

They are almost identical.

Rule of thumb is call them with the parameters as defined (empty list or no list). The compiler will shout at you if you get it wrong, but sometimes you can ignore the compiler.

There is a convention that methods with empty parameters have side effects, but methods without parameters do not have any side effects.



## Method Call Syntax
Operator style vs method call style

`a.b(c) == a b c`

Left associative and right associative methods.

Usually we are right associative, which means we write

`object.method(param)`

or in operator style

`object method param`

Some methods are left associative, which means we write, in operator style

`param method object`

If a method name ends with a colon it is left associative. The colon points towards the object.

`0 :: List(1, 2, 3)`



## Function Literal shorthand
_.country == x => x.country. Each _ stands for an additional parameter in the function
E.g. _ + _ == (x, y) => x + y
Type inference is particularly bad. If the compiler complains write it out long form
