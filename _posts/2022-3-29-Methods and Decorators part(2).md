---
layout: post
title: "Method and Decorators (Part 2)"
tags: [python, programming]
categories: [Programming]
author:
    name: Yusuf Adel
    link: https://yusufadell.web.app
---

# Writing Decorators

As mentioned, decorators are often used when refactoring repeated code
around functions. Consider the following set of functions that need to check
whether the username they receive as an argument is the admin or not and,
if the user is not an admin, raise an exception:

```python
class Store:
    def get_food(self, username, food):
        if username != 'admin':
            raise Exception("This user is not allowed to get food")
        return self.storage.get(food)

    def put_food(self, username, food):
        if username != 'admin':
            raise Exception("This user is not allowed to put food")
        self.storage.put(food)
```

We can see there’s some repeated code here. The obvious first step to
making this code more efficient is to factor the code that checks for admin
status:

```python
def check_is_admin(username):
    if username != 'admin':
        raise Exception("This user is not allowed to get or put food")

class Store:
    def get_food(self, username, food):
        check_is_admin(username)
        return self.storage.get(food)

    def put_food(self, username, food):
        check_is_admin(username)
        self.storage.put(food)
```

We’ve moved the checking code into its own function u. Now our code
looks a bit cleaner, but we can do even better if we use a decorator.

```python
def check_is_admin(f):
    def wrapper(*args, **kwargs):
        if kwargs.get('username') != 'admin':
            raise Exception("This user is not allowed to get or put food")
        return f(*args, **kwargs)
    return wrapper

class Store:

    @check_is_admin
    def get_food(self, username, food):
        return self.storage.get(food)

    @check_is_admin
    def put_food(self, username, food):
        self.storage.put(food)

```

We define our check_is_admin decorator and then call it whenever
we need to check for access rights. The decorator inspects the arguments
passed to the function using the kwargs variable and retrieves the username
argument, performing the username check before calling the actual func-
tion. Using decorators like this makes it easier to manage common func-
tionality. To anyone with much Python experience, this is probably old hat,
but what you might not realize is that this naive approach to implementing
decorators has some major drawbacks.

Stacking Decorators
You can also use several decorators on top of a single function or method.

```python
def check_user_is_not(username):
    def user_check_decorator(f):
        def wrapper(*args, **kwargs):
            if kwargs.get('username') == username:
                raise Exception("This user is not allowed to get food")
            return f(*args, **kwargs)
        return wrapper
    return user_check_decorator

class Store:
    @check_user_is_not("admin")
    @check_user_is_not("user123")
    def get_food(self, username, food):
        return self.storage.get(food)
```

Here, `check_user_is_not()` is a **factory function** for our decorator user​
`_check_decorator()`. It creates a function decorator that depends on the
username variable and then returns that variable. The function `user_check​_decorator()` will serve as a function decorator for `get_food()`. The function `get_food()` gets decorated twice using check_user_is_not().

The question here is which username should be checked first—admin or user123?
```python
class Store:
    def get_food(self, username, food):
        return self.storage.get(food)

Store.get_food = check_user_is_not("user123")(Store.get_food)
Store.get_food = check_user_is_not("admin")(Store.get_food)
```

The decorator list is applied from top to bottom, so the decorators
closest to the def keyword will be applied first and executed last. In the
example above, the program will check for admin first and then for user123.

In the part 3 we'll see if  It’s also possible to implement class decorators
