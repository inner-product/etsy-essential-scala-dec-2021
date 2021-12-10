# Essential Scala for CDP Day 2

## Algebra of Algebraic Data Types

a + (b * c) == (a + b) * (a + c)

Distributive law.

(Algebraic data types are rings)


```scala
// z = a + d
// d = b * c
sealed Z
final case class A() extends Z
final case class D(b: B, c: C) extends Z

final case class Z(d: D, e: E)
sealed trait D
final case class A() extends D
final case class B() extends D

sealed trait E
final case class A2() extends E
final case class C() extends E
```

Data type called a "zipper" that is a derivative of an algebraic data type.


## Option

Option is an algebraic data type.

Option of A is
- Some containing a value of type A or
- None (which contains no value)

Some(1) creates an Option (a Some in particular) that holds an Int
None creates an Option that holds no value


## Reification

Reification: make abstract things concrete
In programming: turn methods into data

```scala
object Calculator {
  def add(left: Double, right: Double): Double = left + right
  def multiply(...) = ...
}
```

Reification allows us to supply different interpretations for a given representation.


## Following the Types

Use the types of input and outputs to guide the implementation


## Recursion in Structural Recursion

When the data is recursive the method is also recursive on that data.


## Scala Language

sealed: means you can only extend within the file in which the sealed thing (trait or class) is defined
final: means cannot be extended anywhere
case class: class with additional stuff (see Essential Scala)
class vs abstract class vs trait:
- class is a template for constructing objects. Can create *instances* of a class, which are objects.
- abstract class is a class that you cannot create instances of; only used for extending
- trait is an abstract class without a constructor
- a class can only extend one other class but can extend multiple traits
- traits and abstract class can have abstract methods: methods that define a signature (parameters and result type) but no implementation

(In Scala 3 traits have constructors)
## Functions and Generic Types
Type variables stands for a specific type that the user chooses when they use the thing (often a collection) with a type variable.

Concretely, `List[A]` means a `List` holding a type `A`, where `A` is chosen by the user. E.g. `List[Int]`, `List[Bookings]`, `List[Purchases]`.

Synonyms: type variable = generic type

A generic type stands for *any* type. It is not constrained in any way---we cannot restrict the user to choosing a subset of types. 
- at the point of definition we don't know what type the user will choose so we can't call any methods on values of that type.
- there are ways to constrain the user's choice: context bounds, and other bounds that I cannot remember the name of (and hardly ever use.)

Functions in Scala:
- are not methods; they are objects
- can convert a method to a function by following the method name with _
- function types: `ParamType => ResultType` or `(ParamType1, ParamType2, ...) => ResultType`
- function literals: `x => x + 1` or `(x, y) => x + y`
- function application is calling the `apply` method
- Scala syntax: if we call a method named `apply` we don't need to explicitly name it. We can call the method "as a function".

Generic types:
- introduce the type
- use the type

Introducing (declaring) a generic type
- on a class / trait or on a method
- declare within square brackets `[A]`
- by convention single upper case letter (but don't be afraid to be more descriptive)

Use:
- a type for a parameter or value, just refer to it as usual
- a type for declaring something with a generic type or extends something with a generic type, they go within `[]`

```scala
final case class Box[A](value: A) {
  def map[B](f: A => B): Box[B] = {
    val theResult: B = f(value)
    Box(theResult)
  }
}
```
