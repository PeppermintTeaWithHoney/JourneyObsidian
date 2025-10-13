2025-10-13 14:07

Status:

Tags:[[Functional Programming]], [[Programming]]

# Pure Functions

Pure functions are really useful because they have no side effects and they always return the same result given the same arguments.



## Reference vs Value

There are a few things that get used via reference and we should make a copy of it if we don't wanna change the original.

For example:

Lists,Dictionaries and Sets are passed by reference and we should make a copy of it.

Some other things are passed by value for example:

Int's,Floats,Strings,boolean and tuples


Rule of thumb is:

Most collection types are passed by reference and most primitive  types are passed by value (except for tuples.)

Mutable:

```py
def modify_list(inner_lst):
    inner_lst.append(4)
    # the original "outer_lst" is updated
    # because inner_lst is a reference to the original

outer_lst = [1, 2, 3]
modify_list(outer_lst)
# outer_lst = [1, 2, 3, 4]
```

Immutable:

```py
def attempt_to_modify(inner_num):
    inner_num += 1
    # the original "outer_num" is not updated
    # because inner_num is a copy of the original

outer_num = 1
attempt_to_modify(outer_num)
# outer_num = 1
```


# Pass by Reference Impurity


Because some types are passed by reference in python we can end up mutating things we don't want to. So we can just make a copy of the types and work with it without changing the value


Pure function:

```py
def remove_format(default_formats, old_format):
    new_formats = default_formats.copy()
    new_formats[old_format] = False
    return new_formats
```

Impure function:

```py
def remove_format(default_formats, old_format):
    default_formats[old_format] = False
    return default_formats
```



## Input and Output ( I/O)


In terms of computing it stands for everything that acts with the outside "world" aka just every thing that's not stored in memory.

Examples of I/O:

- Reading from or writing to a file on the hard drive
- Accessing the internet
- Reading from or writing to a database
- Even simply _printing to the console_ is considered i/o!

_All i/o is a form of "side effect"._















# References
