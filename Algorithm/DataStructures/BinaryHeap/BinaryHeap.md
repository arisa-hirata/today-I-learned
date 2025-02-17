# Binary Heap

## WHAT IS A BINARY HEAP?

__Very__ similar to a binary search tree, but with some different rules!　　

In a __MaxBinaryHeap__, parent nodes are always larger than child nodes. In a __MinBinaryHeap__, parent nodes are always smaller than child nodes. 

## MAX BINARY HEAP
- Each parent has at most two child nodes
- The value of each parent node is __always__ greater than its child nodes
- In a max Binary Heap the parent is greater than the children, but there are no guarantees between  sibling nodes.
- A binary heap is as compact as possible. All the children of each node are as full as they can be and - left children are filled out first

## Why do we need to know this?
Binary Heaps are used to implement Priority Queues, which are __very__ commonly used data structures  

They are also used quite a bit, with __graph traversal__ algorithms

## Big O of Binary Heaps
Insertion - __O(log N)__  
Removal - __O(log N)__  
Search - __O(N)__

## RECAP
- Binary Heaps are very useful data structures for sorting, and implementing other data structures like priority queues
- Binary Heaps are either MaxBinaryHeaps or MinBinaryHeaps with parents either being smaller or larger than their children
- With just a little bit of math, we can represent heaps using arrays!
