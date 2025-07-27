+++
title = "Branchless Partitioning with Hoare & Lomuto"
author = ["Derek"]
date = 2025-07-27
draft = true
+++

I had an opportunity to implement the quickselect algorithm recently. It was a good refresher of.

Paritioning is one of the steps


## Naive {#naive}

One of the naive solutions might to pick a pivot, and iterate through it to construct a \`[left]\` and \`[right]\` list.
Then assign this concatenated list back to the original list variable. Surely there's a better in place solution than:

```python
pivot_value = 5
left = []
right = []
for i in range(arr):
    if i <= pivot_value:
        left += [i]
    else:
        right += [i]
arr = left + right
```


## Hoare {#hoare}

When quick sorting
