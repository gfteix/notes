---
title: Algorithms
description:
aliases:
tags:
created-date: 2025-08-25
---



# Big O
Is a way to categorize the algorithm time or memory requirements based on input. It is not meant to be an exact measurement.

As your input grows, how fast does computation or memory grow?

In languages like Go or Javascript you pay even havier penalties because the memory can be kept araoung; it grows faster, and causes complete halts in your program for cleanup.

- growth is with respect to the input
- constants are dropped
- worst case is usually the way we measure


O(1), O(log n), O(n), O(n log n), O(n^2), O(2^n), O(n!)




O(n)
Example: A loop through N

O(2n) = O(n)
Example: two (independent) loops thorugh n, we drop the constants so it becomes O(n)

O(n^2)
Example: A loop inside a loop 

O(n^3)
Example: A loop inside a loop inside another loop

O(n log n)
Example: Quicksort

O(log n)
Example: Binary search trees

O(sqrt(n))
?

# Arrays Data Structure
contiguous memory space.


```javascript
const a = new ArrayBuffer(6) 

console.log(a) // ArrayBuffer { [Uint8COntents]: <00 00 00 00 00>, byteLength: 6 }

const a8 =  

...

```

- ArrayBuffer is a contiguous piece of memory we can create in Javascript
- We can create a view into this data: Uint8Array -> 8 bits array