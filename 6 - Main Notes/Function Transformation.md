2025-10-29 16:23

Status:

Tags: [[Functional Programming]], [[Programming]]


# Function Transformation

Function transformation is just a more specific way to call a higher order function that takes a function(s) as input and returns a new function.



```py
def multiply(x, y):
    return x * y

def add(x, y):
    return x + y

def self_math(math_func):
    # inner_func is defined inside self_math.
    # It can only be referenced directly
    # inside self_math's scope. However, it is then
    # returned and can be captured into a new variable
    # like square_func or double_func, and called that way
    def inner_func(x):
        return math_func(x, x)
    return inner_func

square_func = self_math(multiply)
double_func = self_math(add)

print(square_func(5))
# 25

print(double_func(5))
# 10
```


# Why Transform?

You might be wondering:

- "When would I use function transformations in the real world?"
- "Isn't it simpler to just define functions at the top level of the code, and call them as needed?"

Good questions. To be clear, we don't just transform functions at [runtime](https://en.wikipedia.org/wiki/Execution_\(computing\)#Runtime) for the fun of it! We only use advanced techniques like function transformations when they make our code _simpler than it would otherwise be_.
















# References
