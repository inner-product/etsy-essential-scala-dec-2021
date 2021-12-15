# Essential Scala for CDP Day 5

## Variance

Variance is denoted by a + or - annotation on the declaration of a type variable.
- + means covariant
- - means contravariant
- if no annotation it is invariant

Variance is about subtyping relationship. In particular, given some subtyping relationship between A and B, what is the subtyping relationship between F[A] and F[B]?

Concretely, imagine Cat <: Animal, Siamese <: Cat. What is the relationship between, say, List[Cat] and List[Animal]?

A <: B (A is a subtype of B) if A can be used in any place where B is required.

Three possible relationships:
- subtype
- supertype
- no relationship

List is *covariant*, means that if A <: B, List[A] <: List[B]
- the subtyping relationship between F[A] and F[B] varies in the same way as A and B

catCleaner: Cat => Clean
animalCleaner: Animal => Clean
siameseCleaner: Siamese => Clean

Sparkling <: Clean
Clean <: KidClean

Which of 

  Cat => Sparkling
  Cat => KidClean

is a subtype of

  Cat => Clean?

Functions are *contravariant* in their input.
- (Animal => Clean) <: (Cat => Clean)

Functions are *covariant* in their output

In general:
- inputs are contravariant
- outputs are covariant

Invariance means there is no relationship between F[A] and F[B] no matter the subtyping relationship between A and B. This is the default.

bananas: Array[Banana]
fruit: Array[Fruit]

Arrays are mutable! Is it safe to pass Array[Banana] to a method expecting Array[Fruit]?

```scala
def fruitBowl(fruit: Array[Fruit]): Unit =
  fruit(0) = cherry // assigning element 0
```

No! Arrays, being mutable, must be invariant.

(Java had this bug when generics were first introduced!)

Variance is never necessary but it makes things more pleasant.


## Unit

Return this when you have nothing meaningful to return. Indicates you're doing side effects. Literal value is written `()`.


## Joins

```scala
df1.join(df2, columnExpr)
df1.join(df2, columnExpr, joinType)
```

`columnExpr` is the condition you're joining on.

`joinType` is a `String` (where are the types?!?!?!?!?!?), one of:
- inner
- cross
- outer
- full
- fullouter
- left
- leftouter
- right
- rightouter
- semi
- leftsemi
- anti
- leftanti


## Working with Missing Values

`df.na`

Three valued logic is annoying. `isnull` to find missing values.


## Execution Plans and Optimization

- Performance model
- explain
- repartitioning
- caching
- join hints


## TODO
- slides
- code walkthrough
- Euclidean distance problem
- show optimization actually doing something
- window example
- Data generation
