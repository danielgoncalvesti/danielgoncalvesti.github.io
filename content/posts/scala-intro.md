---
title: 'Scala for Java Developers'
last_modified_at: 2018-03-20T16:01:04-04:00
categories:
  - blog
tags:
  - Scala
  - Java
toc: true
toc_label: 'Table of Contents'
author:
    'Daniel G.' 
date: 2018-06-02
---

The purpose of this article is not to compare Java with Scala, even because each one uses different paradigms. So while the first one is objected-oriented programming, the another one is funcional programming (but it also works objected-oriented). First of all, what I am going to try to describe here it is my perspective as a Java developer learning Scala language.
Basically, programmers who already know paradigms and concepts about funcional programming such as pure functions, recursion and higher-order functions before to start with Scala, will have greater ease to understand the concepts of the language. I actually say that because at some moment I have decided to follow this order: to learn the concepts and then to apply those concepts to the Scala language, so this way works to me.

## Why Scala?

Scala definitely has many advantages when compared to Java in terms of easiness to use concurrency, optimitization of code complexity and concise notation, among others. In Scala, we can do all the stuff that we do in Java and more something else, so it's like a Java++.

## Some Curiosities

- The semicolons are missing
- The public access modifier is missing
- The declaration of main and functions start with def

<!---## My Experience--->

<!---## Let's try some codes --->

### Immutable and Mutable

Scala supports both mutable and immutable values and collections. For using a multithread program, an immutable value can be a safer option because it can never change after the first assignment. So, we can ensure that another process cannot change that value anymore.

- **var**: used to mutatable values

```scala
var name = "Daniel"
name = "Daniel Goncalves"
name: String = Daniel Goncalves
```

- **val**: used to immutable values

```scala
val name = "Daniel"
name = "Daniel Goncalves"
<console>:8: error: reassignment to val
    name = "Daniel Goncalves"
         ^
```

<!---###  Defining function

```scala
val func = (x: String) => x.length

def func(x: String): Int = s.length

//OR using automatic type inference
def func(x: String) = s.length
```--->

### Type Inference

Scala has a built-in type inference mechanism which allows the programmer to omit certain type annotations. It is, for instance, often not necessary in Scala to specify the type of a variable, since the compiler can deduce the type from the initialization expression of the variable

```scala
val x = 1 + 2 * 3         // the type of x is Int
val y = x.toString()      // the type of y is String
def succ(x: Int) = x + 1  // method succ returns Int values
```

In scala all type inference is local. Scala considers one expression at a time. For example:

```scala
val foo = "word" //OR val foo: String = "word"
val listOfSomething = List(1,2,3) //OR val listOfSomething: List[Int] = List(1,2,3)

```

<!---## Features--->
