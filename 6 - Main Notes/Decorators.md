2025-11-17 14:58

Status:

Tags: [[Functional Programming]] , [[Programming]]


# Decorators

Its just a different syntax for taking a function and returning a function with new behavior. 


```py
def vowel_counter(func_to_decorate):
    vowel_count = 0
    def wrapper(doc):
        nonlocal vowel_count
        vowels = "aeiou"
        for char in doc:
            if char in vowels:
                vowel_count += 1
        print(f"Vowel count: {vowel_count}")
        return func_to_decorate(doc)
    return wrapper

@vowel_counter
def process_doc(doc):
    print(f"Document: {doc}")

process_doc("What")
# Vowel count: 1
# Document: What

process_doc("a wonderful")
# Vowel count: 5
# Document: a wonderful

process_doc("world")
# Vowel count: 6
# Document: world
```


##  Args and Kwargs

In python Args and Kwargs lets us deal with a variable amount of arguments. 
 *args collects positional arguments into a tuple
**kwargs collects keyword (named) arguments into a dictionary

so for arg the position you input them matter
and for kwargs it doesn't

### Positional Arguments
Positional arguments are the ones you're already familiar with, where the order of the arguments matters. Like this:


def sub(a, b):
    return a - b

a=3, b=2
res = sub(3, 2)
res = 1

### Keyword Arguments
Keyword arguments are passed in by name. Order does not matter. Like this:

def sub(a, b):
    return a - b

res = sub(b=3, a=2)
res = -1
res = sub(a=3, b=2)
res = 1

### A Note on Ordering
Any positional arguments must come before keyword arguments. This will not work:

sub(b=3, 2)



## Decorators

Thats why the * arg and ** kwarg is great for working with decorators that uses functions with different signatures. 

The log_call_count function below doesn't care about the number or type of the decorated function's (func_to_decorate) arguments. It just wants to count how many times the function is called. However, it still needs to pass any arguments through to the wrapped function.

def log_call_count(func_to_decorate):
    count = 0

    def wrapper(*args, **kwargs):
        nonlocal count
        count += 1
        print(f"Called {count} times")
        # The * and ** syntax unpacks the arguments
        # and passes them to the decorated function
        return func_to_decorate(*args, **kwargs)

    return wrapper
    




# References
