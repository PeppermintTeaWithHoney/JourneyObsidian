22025-10-09 15:08

Status: Ongoing

Tags:  [[Programming]] [[Functional Programming]]


# Functional Programming

Functional programming is a paradigm that makes us write new functions instate of mutating a state(updating values).

Functional programming is more about what you want to happen instead of how.

Imperative declares both the how and the what.

Example of imperative code:

```py
car = create_car()
car.add_gas(10)
car.clean_windows()
```

Example of functional code:

```py
return clean_windows(add_gas(create_car()))
```


## Immutability 

In functional programming we strive to make the value immutable, aka we don't wanna change the value with functions. Its easier to work with because we always know what value the function has.

Tuples vs list for example. We know the tuple won't be changed because its immutable, a list on the other hand get changed so its mutable. 


```python
ages = [16, 21, 30]
# 'ages' is being changed in place
ages.append(80)
# [16, 21, 30, 80]
```

Here we editing the list and appending a new number.

```python
ages = (16, 21, 30)
more_ages = (80,) # note the comma! It's required for a single-element tuple
# 'all_ages' is a brand new tuple
all_ages = ages + more_ages
# (16, 21, 30, 80)

# or we can even reassign the same variable to point to a new tuple:
ages = ages + more_ages
# (16, 21, 30, 80)
```


Here we make a complete new tuple.


## Declarative programming

In functional programming we strive to be more declarative, we want see what is going on instead of the how.

Example of declarative CSS code:

```css
button {
  color: red;
}
```

The same example in a imperative way in Python:

```py
from tkinter import * # first, import the library
master = Tk() # create a window
master.geometry("200x100") # set the window size
button = Button(master, text="Submit", fg="red").pack() # create a button
master.mainloop() # start the event loop
```




## Functions vs classes?

Which one is better? None is better, they are just different and it depends on the situation. Rule of thumb, if i don't know how which one to use, i will default to functions.

If i want something stateful and more long-lived i can use a Class, its also easier to share behavior via inheritance.

Classes make you think about the world as a bundle of objects that bundle behavior,data and state together in a way that draws boundaries between instances of things, like chess pieces on a board.

Functions makes you think about a the world as a series of data transformations. Functions can take multiple things as input  return a transformed output. It could return a whole state of a chessboard where you input the individual moves as inputs.


## Debugging Functional Programming



It's impossible to write perfect code the first time, everyone has to debug their code, from a senior to a junior developer. That's why debugging is such a important skill to have especially when you have elegant one-liner like this:

```py
def get_player_position(position, velocity, friction, gravity):
    return calc_gravity(calc_friction(calc_move(position, velocity), friction), gravity)
```


If something goes wrong it will be really hard to debug this, the other options is just to break it up like this:

```py
def get_player_position(position, velocity, friction, gravity):
    moved = calc_move(position, velocity)
    slowed = calc_friction(moved, friction)
    final = calc_gravity(slowed, gravity)
    print("Given:")
    print(f"position: {position}, velocity: {velocity}, friction: {friction}, gravity: {gravity}")
    print("Results:")
    print(f"moved: {moved}, slowed: {slowed}, final: {final}")
    return final
```

now we can use print statements to debug this



## Functional Programming vs Object Oriented Programming

One isn't better than the other, they don't even contradict themselves, besides inheritance. A good programmer knows both of them and when to use one over the other.


## Statement vs Expressions 

Statements are actions to be carried out for example:

```py
n = 7  # Variable assignment statement

def greet(name):  # Function definition statement
    return f"Hello, {name}!"

if x > 10:  # `if` statement
    print(greet("Alice"))

for i in range(n):  # `for` loop statement
    print(i)
```

Every complete instruction is a statement.

Expressions are a subset of statements and always produce a value. That means we can use that however we need it.

```py
result = 2 + 2  # Arithmetic expression
length = len("hello")  # Function call expression
total_cost = len(items) * cost  # Multiple expressions combined into one
```


## Ternary Expressions

Ternary Expressions get used to combine a few if else statements into one line

Normal:
```py
result = 0
if number % 2 == 0:
    result = number / 2
else:
    result = (number * 3) + 1
```


With Ternary:
```py
result = number / 2 if number % 2 == 0 else (number * 3) + 1
```








# References

Boot.dev functional programming course