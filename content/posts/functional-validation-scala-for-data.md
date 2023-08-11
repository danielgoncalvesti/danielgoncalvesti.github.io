---
title: 'Enhancing Data Validation with Either in Scala: A Journey Through Reliable Code'
last_modified_at: 2018-03-20T16:01:04-04:00
categories:
  - blog
tags:
  - scala
  - validation
  - data validation
  - either
  - validation-domain
toc: true
toc_label: 'Table of Contents'
author:
  'Daniel G.'
date: 2023-08-11
---

As a Scala developer, you'll inevitably encounter the necessity for validation while handling domain models. The Scala ecosystem presents an extensive array of tools tailored for this exact purpose. In this blog post, we'll delve into several prevalent approaches, demonstrating their application to a domain model.
  
Data validation is a fundamental aspect of building robust software systems, ensuring that the input adheres to specific criteria. In Scala, the functional programming paradigm, coupled with the `Either` type, provides a powerful mechanism for handling validation while preserving the purity and composability of functional programming. In this blog post, we'll explore how to leverage the `Either` type to create reliable and maintainable validation code in Scala.

## The `Either` Type in Scala

The `Either` type is a fundamental building block in functional programming, representing a value that can be either of two possible types: `Left` or `Right`. The convention is to use `Left` for failures (often representing an error message) and `Right` for successes (the valid value). This dual nature of `Either` makes it perfect for handling validation outcomes, as we can use `Left` to capture errors and `Right` to hold valid results.

## Benefits of Using `Either` for Validation

Using `Either` for validation offers several advantages:

1. **Explicit Error Handling**: By convention, errors are explicitly represented as `Left` values, making it clear that validation has failed and providing a place to include detailed error information.

2. **Composability**: You can compose multiple validation steps using functional constructs, allowing you to build complex validation pipelines while keeping the code readable and modular.

3. **Immutable**: Like other functional constructs in Scala, `Either` is immutable. Validation functions don't modify the original data, promoting predictability and reducing side effects.

4. **Pattern Matching**: Pattern matching can be used to handle both success and failure cases elegantly, making it easy to control the flow based on validation outcomes.

## Practical Example: Validating a User's Age and Email

Let's consider a simple example where we want to validate a user's age and email during the registration process. We'll define validation functions for age and email, and then compose them to validate the user registration.

```scala
case class UserRegistration(email: String, age: Int)

object UserValidation {
  type ValidationResult[A] = Either[String, A]
  
  def validateRegistration(user: UserRegistration): ValidationResult[UserRegistration] =
	  def validateAge(age: Int): ValidationResult[Int] =
	    if (age >= 18 && age <= 99)
	      Right(age)
	    else
	      Left("Age must be between 18 and 99")

	  def validateEmail(email: String): ValidationResult[String] =
	    if (email.matches("^[A-Za-z0-9+_.-]+@(.+)$"))
	      Right(email)
	    else
	      Left("Invalid email format")

	  for {
	    validEmail <- validateEmail(user.email)
	    validAge <- validateAge(user.age)
  	  } yield UserRegistration(validEmail, validAge)
}
```

In this example, the `validateAge` and `validateEmail` functions return `Either` values. If the validation succeeds, a `Right` value is returned, containing the validated data. If the validation fails, a `Left` value is returned, containing the error message.

The `validateRegistration` function demonstrates how to compose the individual validation steps using a for-comprehension. If both email and age validation succeed, it constructs a `Right` value with the validated `UserRegistration`. If any validation fails, the first encountered `Left` value is returned, containing the appropriate error message.

## Handling Validation Results

Once you have the validation result, you can use pattern matching or other functional constructs to handle the outcomes in your application code. Here's an example of how you might handle the result of a user registration validation:

```scala
val userToRegister = UserRegistration("example@email.com", 25)
val validationResult = UserValidation.validateRegistration(userToRegister)

validationResult match {
  case Right(validUser) => println(s"Successfully registered: $validUser")
  case Left(errorMessage) => println(s"Registration failed: $errorMessage")
}
```

This pattern matching approach allows you to handle both success and failure cases explicitly, ensuring that your application responds appropriately based on the validation result.


Leveraging the `Either` type in Scala enables you to build reliable and flexible data validation pipelines. By embracing functional programming principles and composing validation functions using `Either`, you create code that is explicit, composable, and robust. Whether you're validating user input, API requests, or any other data, using `Either` for validation in Scala is a powerful strategy that enhances the reliability and maintainability of your software systems.
