# Essential Scala for CDP
## Introductions

- Name, programming background, issues w/ Scala or things you want to learn how to do

Noel, Scala for about 10 years, a variety of other PLs. PL / ML / teaching

Arie: MySQL DBA, long time service at Etsy (10+ years!) Learn more about big data. Maybe move into ML / big data. Lots of scripts. Python, Bash, but not pure SE. No JVM.

Johannes: Data scientist on product analytics. BigQuery, Python, MySQL dialects. A little bit of Scala. Learn fundamentals so can take Scala and apply it on big data applications.

Han: Senior Applied Scientist. Lots of Python. 2 days Scala training. Data transformation & ETL. FP.

Vineet: Data scientist. Big Query etc. 

Cedric: Staff Applied Scientist in CV. Computer vision before & after deep learning. C programming. Python. ML. Joined Etsy in April. Scala to access data. Adjust C mindset to FP.

Eliel: 6 months at Etsy. Almost exclusively Scala. Lots of JS / Python. Treating Scala as JS / Python. Gain a better understanding of Scala / Spark.

akachler@etsy.com
jharkins@etsy.com
hanjiang@etsy.com
ehernandez@etsy.com
cbeliard@etsy.com
vkarkhanis@etsy.com

## Course Overview

### Notes & Learning


### Admin

Times & breaks


### Curriculum

Setup and Basic Workflow
Expressions, Types, and Values
Algebraic Data Types
Sequencing Computations
Spark Fundamentals


### How We Teach

Models and processes
- Build mental models to understand how things work
- Learn processes to understand how to do things


### Additional Material

Essential Scala


## Setup

- Essential Exercises: https://github.com/inner-product/essential-exercises 
  - Use the `sbt` project, not the `gradle` one!


sbt
- compile / test / console
- :quit to exit console
- :help for help in the console

Hide the source code in src/main/scala
Tests in src/test/scala
Blame Maven!

project directory contains more sbt configuration


## Expressions, Types, and Values

"Types" in Python and Javascript are not types in Scala.

Expressions
- program text. 1 + 1

Values
- things in the computer's memory

Evaluation (execution, running code)
- Turns expressions into values

(compile time)                (run time)
expressions == evaluation ==> values

Analogy:
- expressions : writing
- evaluation : reading
- values : understanding in the reader's head

Types are a property of expressions, not of values
- A type is a constraint, describes the set of values than an expression could evaluate to.
- Don't exist at runtime (but sometimes we create values that represent types)
- Can't pass information from runtime to compile time

4 / 2 ==> is an Integer!
readAnIntegerFromTheUser() / 4 ==> is a Float!

Double / Int = Double
Int / Double = Double
Implicit numeric conversions are tricky

Mary    bit   the dog
subject verb  object

Mary the dog bit


## General Problem Solving Strategies

- science: empiricism / try stuff out and see what happens / make a hypothesis and test it (debugging)
- logic: reason from a model (you need to have a model)
- appeal to authority! (boo!) (ask a senior dev)

## Algebraic Data Types
Functional programmers value:
- reasoning about code
- composition
- fancy words for simple ideas

Algebraic data types model data that can be expressed in terms of:
- logical ands (product types)
- logical ors (sum types)

[Cedric: it is a ring!]

Order is a Customer and Delivery Details and a collection of Line Items
Shipping Method is Standard or Expedited or Signed For
Delivery Details is Shipping Method and Address

In abstract:
- A is a B and C
- A is a B or C

```scala
// A is a B and C
final case class A(b: B, c: C)

// A is a B or C
sealed trait A
final case class B() extends A
final case class C() extends A
```

Example

Shipping Method is Standard or Expedited or Signed For

```scala
sealed trait ShippingMethod
final case class Standard() extends ShippingMethod
final case class Expedited() extends ShippingMethod
final case class SignedFor() extends ShippingMethod
```

Order is a Customer and Delivery Details and a collection of Line Items

```scala
final case class Order(customer: Customer, delivery: DeliveryDetails, items: List[LineItem])
```

Algebraic data types are a closed world! You cannot extend them without modifying existing code. This gives us some guarantees about correctness (and the compiler helps to enforce these as well)

