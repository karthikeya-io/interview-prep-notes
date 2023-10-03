**Linked List**

A linked list is a data structure used to organize a sequence of elements. Each element in the list is contained in a node. The node consists of two parts: the element itself, and a reference (or link) to the next node in the sequence.

**Types of Linked Lists:**

1. **Singly Linked List**: Each node contains data and a next pointer which points to the next node in line of the list.
2. **Doubly Linked List**: Each node contains data, a pointer to the next node, and a pointer to the previous node.
3. **Circular Linked List**: It can be a singly circular linked list or a doubly circular linked list. The last node of the list points back to the first node (or the previous node in the case of a doubly circular linked list).

**Advantages of Linked List:**

1. **Dynamic Size**: Unlike arrays, linked lists do not have a fixed size. It can grow or shrink during runtime.
2. **Efficient Insertions/Deletions**: Insertion or deletion of a data element at a particular point is more efficient than arrays because it just requires changing the pointers.
3. **No Wasted Memory**: We can allocate memory for linked list nodes as required, unlike arrays which can lead to memory wastage if elements are not used.
4. **Can Store Items with Different Sizes**: An element can be an object (or a reference to an object) of varying sizes.

**Disadvantages of Linked List:**

1. **Random Access is Costly**: To access an element, one has to iterate from the head of the linked list.
2. **Extra Memory**: For each element, an extra memory space is required for a pointer (two for doubly linked lists).
3. **Not Cache Friendly**: Due to their dynamic memory allocation, linked lists can't leverage the benefits of cache memory.

**Basic Operations on Linked List:**

1. **Insertion**: At the beginning, end, or middle.
2. **Deletion**: Of the first node, last node, or any given node.
3. **Traversal**: Go through each element of the list.
4. **Searching**: Find a particular data element in the list.
5. **Update**: Modify the current data of a node.

**Common Techniques and Concepts**:

1. **Two Pointers**: Similar to arrays but often used to detect a cycle in a linked list or find the midpoint.
2. **Reversing a Linked List**: Iterative and recursive methods exist to reverse a linked list.
3. **Merging Two Sorted Linked Lists**: This technique is useful, especially in merge sort on linked lists.
4. **Detecting Loop**: Floyd's Cycle-Finding algorithm (Tortoise and the Hare approach) can be used to detect loops.
5. **Finding the Starting Point of Loop**: Once the loop is detected using the Tortoise and the Hare approach, there are methods to find the start of the loop.
6. **Finding the nth node from the end**: Use two pointers – one moving ahead by n nodes first and then both moving till the end.
7. **Use of Dummy Node**: Especially useful to simplify edge cases in problems where the head of the list might change.

**Example: Singly Linked List Node in Java**:

```java
class ListNode {
    int val;
    ListNode next;

    ListNode(int x) {
        val = x;
        next = null;
    }
}
```

When solving problems with linked lists, understanding the nature of the problem, visualizing, and drawing out the linked list can be very helpful. It's also crucial to be mindful of null pointers and handle edge cases, as they can lead to runtime errors.
