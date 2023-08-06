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

![scala-logo](/img/scala-logo.png)

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
&nbsp;

### Error Handling
Error handling in Scala is essential for writing robust and reliable code. Scala provides several mechanisms for dealing with errors, and three popular approaches are using Option, Try, and Either.
&nbsp;

#### Option
Option is a container that represents an optional value, meaning it can hold either `Some(value)` or `None`. It is widely used to handle scenarios where a function may not return a valid result.

Let's consider an example of using Option to handle the absence of a value:
```scala
def findElementById(id: Int): Option[String] = {
  // Database lookup logic here
  // Return Some(result) if the element is found, otherwise None
  if (id == 1) Some("Found element")
  else None
}

val elementId = 1
val result: Option[String] = findElementById(elementId)

// Pattern matching to handle the Option
val message: String = result match {
  case Some(value) => value
  case None => "Element not found"
}

println(message) // Output: "Found element"
```
&nbsp;

#### Try
Try is a container that represents a computation that may result in a value or an exception. It is useful for handling functions that may throw exceptions.
```scala
import scala.util.Try

def divide(a: Int, b: Int): Try[Int] = Try {
  if (b != 0) a / b
  else throw new ArithmeticException("Division by zero is not allowed.")
}

val result1: Try[Int] = divide(10, 2) // Success(5)
val result2: Try[Int] = divide(10, 0) // Failure(java.lang.ArithmeticException: Division by zero is not allowed.)

// Pattern matching to handle the Try
val output1: String = result1 match {
  case scala.util.Success(value) => s"Result: $value"
  case scala.util.Failure(exception) => s"Error: ${exception.getMessage}"
}

val output2: String = result2 match {
  case scala.util.Success(value) => s"Result: $value"
  case scala.util.Failure(exception) => s"Error: ${exception.getMessage}"
}

println(output1) // Output: "Result: 5"
println(output2) // Output: "Error: Division by zero is not allowed."
```
&nbsp;

#### Either
Either is a container that represents a value of one of two possible types: Left or Right. It is often used when we want to handle multiple error types.
Consider an example of using Either to handle different types of errors:
```scala
def divide(a: Int, b: Int): Either[String, Int] = {
  if (b != 0) Right(a / b)
  else Left("Division by zero is not allowed.")
}

val result1: Either[String, Int] = divide(10, 2) // Right(5)
val result2: Either[String, Int] = divide(10, 0) // Left("Division by zero is not allowed.")

// Pattern matching to handle the Either
val output1: String = result1 match {
  case Right(value) => s"Result: $value"
  case Left(errorMessage) => s"Error: $errorMessage"
}

val output2: String = result2 match {
  case Right(value) => s"Result: $value"
  case Left(errorMessage) => s"Error: $errorMessage"
}

println(output1) // Output: "Result: 5"
println(output2) // Output: "Error: Division by zero is not allowed."
```
I understand that the three error handling methods might be confusing regarding when to use each one. To clarify, here are the best practices for utilizing each of them in different situations:
- Use `Option` for cases where a function may return a value or None.
- Use `Try` for handling potentially throwing functions and capturing exceptions.
- Use `Either` for handling different types of errors and providing meaningful error messages.

To conclude the topic, Scala provides powerful constructs like Option, Try, and Either to handle errors effectively and promote more predictable and maintainable code. Understanding the differences between these constructs and adopting best practices for error handling can significantly enhance the reliability and usability of Scala applications.
\
&nbsp;

I believe this post provides a brief overview of the Scala language. In the next post, I will delve into more advanced Scala language concepts. Stay tuned!

