2025-11-23 12:46

Status: Ongoing

Tags: [[Math]], [[Data Structures and Algorithms]]

# Big O Notation

Big O analysis is one of the ways to compare the time complexity of algorithms and with that their practicality. 

We write Big-O notation like this:
```
O(formula)
```

Where `formula` describes how an algorithm's run time or space requirements grow **as the input size grows.**

- `O(1)` - constant
- `O(log n)` - logarithmic
- `O(n)` - linear
- `O(n^2)` - squared
- `O(2^n)` - exponential
- `O(n!)` - factorial


![[Pasted image 20251123164340.png]]

O(n) is very common. That's when the number of steps grows the same rate as its input size.

```py
def find_max(nums):
    max = float('-inf')
    for num in nums:
        if num > max:
            max = num
    return max
    
```





## Constants don't matter

Big-O notation only cares about the theoretical growth rate of algorithms not the time itself. 


## Order of 1

O(1) means no matter the size of the input, there is no growth in the runtime of the algorithm.


## Order Log N


O(log(n)) are only slightly slower than O(1) algorithms, but much faster than 0(n). The grow according to the input size, n,n but only according to the log of it.


`O(n)`:

|n|time|
|---|---|
|8|8 ms|
|64|64 ms|
|1024|1024 ms|
|1048576|1048576 ms|

`O(log(n))`:

| n       | time  |
| ------- | ----- |
| 8       | 3 ms  |
| 64      | 6 ms  |
| 1024    | 10 ms |
| 1048576 | 20 ms |




















