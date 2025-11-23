2025-11-21 18:48

Status: Ongoing

Tags: [[Math]]

# Logarithms


A logarithm is the inverse of an exponent.

24 = 16

log216 = 4

"log216" can be read as "log base 2 of 16", and means "the number of times 2 must be multiplied by itself to equal 16".

"log216" might also be written as `log2(16)`

Some more examples:

| Logarithm   | Result |
| ----------- | ------ |
| log2 2      | 1      |
| log2 4      | 2      |
| log2 8      | 3      |
| log2 16     | 4      |
| log10 10    | 1      |
| log10 100   | 2      |
| log10 1000  | 3      |
| log10 10000 | 4      |


![[Pasted image 20251121185139.png]]







Exponents grow very quickly, and **logarithms grow very slowly.** A logarithm is the _inverse of an exponent_.


![[Pasted image 20251121190053.png]]


Generally speaking, it's nice when we can write code that uses `log(n)` time to run, where `n` is the amount of data to process. For example, let's say we have a list of `1,000,000` users, and we want to write an algorithm that finds the user with the most followers.

If it takes `1` millisecond to check one user (let's just pretend), a linear algorithm would take `1,000,000` milliseconds, or about `16` minutes and `40` seconds.

A quadratic algorithm (exponent) would take `1,000,000,000,000` milliseconds, or about `31.7` years.

However, a logarithmic algorithm would only take `20` milliseconds! Here's a table to illustrate the difference:

|Input Size|Linear (`n*2`)|Quadratic (`n^2`)|Log (`log2(n)`)|
|---|---|---|---|
|10|20 ms|100 ms|3 ms|
|100|200 ms|10,000 ms|7 ms|
|1,000|2,000 ms|1,000,000 ms|10 ms|
|10,000|20,000 ms|100,000,000 ms|14 ms|
|100,000|200,000 ms|10,000,000,000 ms|17 ms|
|1,000,000|2,000,000 ms|1,000,000,000,000 ms|20 ms|


# References
