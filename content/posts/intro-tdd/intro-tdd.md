---
title: Introduction to test-driven development (TDD) (Part 1)
description: Is it right for my development workflow?
date: 2017-10-21T11:00:00.000Z
---

In this tutorial, I'm going to walk you through how to start using TDD in your development work.

> If am asked to explain TDD in a few words, I'd say TDD is the development of tests before a feature implementation. TDD is also known as Test First Development

I will talk about how to use Java and Junit in the context of TDD, but these are just tools. The main aim of this write up is to give you an understanding of TDD regardless of the programming language and testing framework used.

**TDD workflow:**

1. Write test
2. Run test - test does not pass since there is no implementation code
3. Write just enough implementation code to make the test pass
4. Run tests - tests pass
5. Refactor
6. Repeat

TDD requires a different way of thinking. In order to start TDD you need to forget the way you developed code before. This process is very hard. And it is even harder if you don't know how to write unit tests. But it's worth it.

**Let's start!**

**Create a simple password validator**

_Requirement: The password should be between 6 to 10 characters_

First, we write the test code that fulfils the above requirement.

```java

import org.junit.Assert;
import org.junit.Test;

import static org.junit.Assert.*;

/**
 * @author george
 */
public class TestPassword {
    @Test
    public void testPasswordLength() {
        PasswordValidator validator = new PasswordValidator();
        assertEquals(true, validator.isValid("Abc123"));
    }
}

```

To run the test, we need to create the PasswordValidator class.

```java

/**
 * @author george
 */
class PasswordValidator {
    boolean isValid(String password) {
        return password.length() >= 6 && password.length() <= 10;
    }
}

```

We will run the above test again. The test passes as shown below.

![Test](tdd-pass.png)

You notice that we wrote just enough implementation code to make the test pass.

The next step is to refactor the code.

We can see that in testPasswordLength() method, there is no need for creating an instance of class PasswordValidator. Instance means creating an object of the class to refer the members (variables and methods) of that class. So we refactor and change the code as below:

```java

import org.junit.Assert;
import org.junit.Test;

import static org.junit.Assert.*;

/**
 * @author george
 */
public class TestPassword {
    @Test
    public void testPasswordLength() {
        assertEquals(true, PasswordValidator.isValid("Abc123"));
    }
}
```

Change PasswordValidator class to:

```java

/**
 * @author george
 */
class PasswordValidator {
    static boolean isValid(String password) {
        return password.length() >= 6 && password.length() <= 10;
    }
}
```

We run all the tests again. All the tests are green as shown below:

![Test](tdd-pass-2.png)

> Initially posted at https://obiero-ogada.medium.com

#### Summary

TDD when used properly, the code becomes clearer and simple to understand.

Give TDD a chance
