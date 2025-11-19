2025-11-03 13:48

Status:

Tags: [[Programming]], [[Functional Programming]]


# Currying


Function currying is a specific kind of function transforming that takes a single function that accepts multiple arguments into multiple functions that each accept a single one.



This is a "normal" 3-argument function:

```py
box_volume(3, 4, 5)
```

This is a "curried" _series of functions_ that does the same thing:

```py
box_volume(3)(4)(5)
```


Here's another example that includes the implementations:

```py
def sum(a, b):
  return a + b

print(sum(1, 2))
# prints 3
```

And the same thing curried:

```py
def sum(a):
  def inner_sum(b):
    return a + b
  return inner_sum

print(sum(1)(2))
# prints 3
```



## Why would we use Curry

So why would we ever want to do the more complicated thing? Well, currying is often used to change a function's signature to make it conform to a specific shape. For example:

def colorize(converter, doc):
  # ...
  converter(doc)
  # ...
  

The colorize function accepts a function called converter as input, and at some point during its execution, it calls converter with a single argument. That means that it expects converter to accept exactly one argument. So, if I have a conversion function like this:

def markdown_to_html(doc, asterisk_style):
  # ...

I can't pass markdown_to_html to colorize because markdown_to_html wants two arguments. To solve this problem, I can curry markdown_to_html into a function that takes a single argument:

pydef markdown_to_html(asterisk_style):
  def asterisk_md_to_html(doc):
    # do stuff with doc and asterisk_style...

  return asterisk_md_to_html

markdown_to_html_italic = markdown_to_html('italic')
colorize(markdown_to_html_italic, doc)










# References
