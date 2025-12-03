2025-11-24 14:59

Status:

Tags: [[Journey/3 - Tags/Data Structures and Algorithms|Data Structures and Algorithms]]


# Sorting Algorithms


Almost every action you take on a web app relies on data, which has to be sorted some how.  Just looking up a profile on a social media platform likely relies on a sorted index.


## Bubble Sort

```py
def bubble_sort(nums):
    swapping = True
    end = len(nums)
    while swapping is True:
        swapping = False
        for i in range(1,end):
            if nums[i -1] > nums[i]:
                first = nums[i]
                second = nums[i-1]
                nums[i] = second
                nums[i-1] = first
                swapping = True
        end -= 1
    return nums
            
```

    
 

## Merge Sort

```python
def merge_sort(nums):
    if len(nums) < 2:
        return nums
    first = merge_sort(nums[: len(nums) // 2])
    second = merge_sort(nums[len(nums) // 2 :])
    return merge(first, second)


def merge(first, second):
    final = []
    i = 0
    j = 0
    while i < len(first) and j < len(second):
        if first[i] <= second[j]:
            final.append(first[i])
            i += 1
        else:
            final.append(second[j])
            j += 1
    while i < len(first):
        final.append(first[i])
        i += 1
    while j < len(second):
        final.append(second[j])
        j += 1
    return final
```


Why merge sort?

Pros: Its way faster than bubble sort.. O(n * log(n))
	and its stable. Values with duplicate keys will stay in place.

Cons:
	Memory usage, since we don't only use one array unlike other we use way more memory
	Recursion: It uses Recursion and in lots of languages that tanks the performance, like in python.





## Insertion Sort

Insertion sort builds a list one item at a time, its way less effective than merge sort, but its actually faster on smaller lists.

Insertion sort has a Big O of O(n^2), because that is its worst case complexity.

The outer loop of insertion sort always executes n times, while the inner loop depends on the input.

Best case: If the data is pre-sorted, insertion sort becomes really fast. Can you see why?
Average case: The average case is O(n^2) because the inner loop will execute about half of the time.
Worst case: If the data is in reverse order, it's still O(n^2) and the inner loop will execute every time.



Why use Insertion Sort?

Its fast for very small data sets < 10. Its even faster if they are presorted in some way. Its stable, it doesn't change the relative order of the keys with equal keys. It also only requires a constant amount of memory.  It also can sort a list how it receives it. Its faster on small data sets because it has a low memory footprint and no recursion overhead



## Quick Sort


def quick_sort(nums, low, high):
    if low < high:
        x = partition(nums,low,high)
        quick_sort(nums,low, x -1)
        quick_sort(nums,x +1, high)

def partition(nums, low, high):
    pivot = nums[high]
    i = low - 1
    for j in range(low,high):
        if nums[j] < pivot:
            i += 1
            nums[i], nums[j] = nums[j], nums[i]
    nums[i+1], nums[high] = nums[high], nums[i+1]
    return i + 1

On average the Big O from Quick Sort is O(n*log(n))
but it can degrade.


In the worst case it can degrade to O(n^2), which is really bad.

**Worst case**: The input is already sorted. An already sorted array results in the pivot being the largest or smallest element in the partition each time, meaning `partition()` is called a total of `n` times.

**Best case**: The pivot is the middle element of each sublist which results in `log(n)` calls to `partition()`.



# Fixing Quick Sort

While the version of quicksort that we implemented is almost always able to perform at speeds of `O(n*log(n))`, its Big O is still technically `O(n^2)` due to the worst-case scenario. We can fix this by altering the algorithm slightly.

Two of the approaches are:

- Shuffle input randomly before sorting. This can trivially be done in `O(n)` time.
- Actively find the median of a sample of data from the partition, this can be done in `O(1)` time.

## Random Approach

The random approach is easier to code, which is nice if you're the one writing the code.

The function simply shuffles the list into random order before sorting it, which is an `O(n)` operation. The likelihood of shuffling a large list into sorted order is so low that it's not worth considering.

## Median Approach

Another popular solution is to use the "median of three" approach. Three elements (for example: the first, middle, and last elements) of each partition are chosen and the median is found between them. That item is then used as the pivot.

This approach has less overhead, and also doesn't require randomness to be injected into the function, meaning it can remain deterministic and _pure_.


















# References
