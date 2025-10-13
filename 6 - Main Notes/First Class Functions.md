

2025-10-10 16:44

Status:

Tags: [[Functional Programming]] [[Programming]]


# First Class Functions


## Functions as values

In Python function are just values so we can use them like values. We could write a function that returns 2 integers that are added together and use that in another function.

```py
def add(x, y):
    return x + y

# assign the function to a new variable
# called "addition". It behaves the same
# as the original "add" function
addition = add
print(addition(2, 5))
# 7
```


## Anonymous functions

Anonymous functions have no name and are called lambda functions in python.

```py
lambda x: x + 1
```
Here the result gets returned automatically so there is no need to return it by yourself.
They just return the result of a expression, they are mostly used in small things.

```py
get_age = lambda name: {
    "lane": 29,
    "hunter": 69,
    "allan": 17
}.get(name, "not found")
print(get_age("lane"))
# 29
```




## Map function

Map, filter and reduce are three commonly used higher order functions. With map we don't have to use a loop and can just use a function and a iterable and it returns a iterator that uses the function on every iterable. 

With `map`, we can operate on lists without using loops and nasty stateful variables. For example, given this code:

```py
def square(x):
    return x * x

nums = [1, 2, 3, 4, 5]
squared_nums = []
for num in nums:
    num_squared = square(num)
    squared_nums.append(num_squared)

print(squared_nums)
# [1, 4, 9, 16, 25]
```

We could use `map` instead, like this:

```py
def square(x):
    return x * x

nums = [1, 2, 3, 4, 5]
squared_nums = map(square, nums)

print(list(squared_nums))
# [1, 4, 9, 16, 25]
```



## Filter function

The function takes function and  a iterable (a list for example) and returns a iterator that only contains elements from the original iterable where the result was True.

In Python:

```py
def is_even(x):
    return x % 2 == 0

numbers = [1, 2, 3, 4, 5, 6]
evens = list(filter(is_even, numbers))
print(evens)
# [2, 4, 6]
```



## Functions reduce

The reduce function takes a function and a list of values, and applies the function to each item in the list creating one single result.


```py
# import functools from the standard library
import functools

def add(sum_so_far, x):
    print(f"sum_so_far: {sum_so_far}, x: {x}")
    return sum_so_far + x

numbers = [1, 2, 3, 4]
sum = functools.reduce(add, numbers)
# sum_so_far: 1, x: 2
# sum_so_far: 3, x: 3
# sum_so_far: 6, x: 4
# 10 doesn't print, it's just the final result
print(sum)
# 10
```



## Map, Filter and Reduce


Allow us to avoid stateful iteration and mutations of variables.



```py
def factorial(n):
    # a procedure that continuously multiplies
    # the current result by the next number
    result = 1
    for i in range(1, n + 1):
        result *= i
```

```py
import functools

def factorial(n):
    return functools.reduce(lambda x, y: x * y, range(1, n + 1))
```





# References
