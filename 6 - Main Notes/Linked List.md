
2025-11-27 14:19

Status:

Tags: [[Programming]], [[Journey/3 - Tags/Data Structures and Algorithms|Data Structures and Algorithms]]



# Linked Lists

Remember how the `push` method on our Queue is `O(n)` instead of `O(1)`?

```python
def push(self, item):
    # everything in self.items has to shift
    # up a position, which takes O(n) time
    self.items.insert(0, item)
```

_Let's fix that_.

To build a faster queue, we'll use a [Linked List](https://en.wikipedia.org/wiki/Linked_list) instead of a regular `List` (array) under the hood. A linked list is where elements are _not_ stored next to each other in memory, instead, each item _references_ the next in a chain.




## Linked List vs. List






A linked list is a collection of ordered items, so its similar to a normal list(array in other languages.)

![[Pasted image 20251127173345.png]]


## Iterating













# References
