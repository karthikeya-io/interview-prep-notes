### Introduction

A heap is a specialized tree-based data structure that satisfies the heap property. It is an important structure because it's efficient for priority queue operations, such as insertion, extraction, and deletion.

There are 2 types of heaps min and max. In min heap parent element is always less than child and in max heap parent element is always greater than child.

Here, we'll discuss a binary heap, particularly a min-heap, where the parent node is less than or equal to its children.

Lets learn the following:

1. Heap Implementation
2. Insertion
3. Extract Min
4. Decrease Key
5. Delete

Sure! A heap is a specialized tree-based data structure that satisfies the heap property. It is an important structure because it's efficient for priority queue operations, such as insertion, extraction, and deletion.

Here, we'll discuss a binary heap, particularly a min-heap, where the parent node is less than or equal to its children.

### Heap Implementation

A binary heap can be implemented using a one-indexed array, where each element has:

- A parent at position `i/2`
- A left child at position `2 * i`
- A right child at position `2 * i + 1`

> Note: The root element is at position 1. This is to simplify the implementation. You can also use a zero-indexed array, but you'll have to do some extra calculations. For example, the parent of the element at position `i` is at position `(i - 1) / 2`. The left child of the element at position `i` is at position `2 * i + 1`. The right child of the element at position `i` is at position `2 * i + 2`. In this tutorial, we'll use a one-indexed array.

Here's a simple class for a min-heap:

```java
public class MinHeap {
    private int[] heap;
    private int size;

    public MinHeap(int capacity) {
        heap = new int[capacity + 1];
        size = 0;
    }

    private int parent(int pos) {
        return pos / 2;
    }

    private int leftChild(int pos) {
        return 2 * pos;
    }

    private int rightChild(int pos) {
        return 2 * pos + 1;
    }

    private void swap(int firstPos, int secondPos) {
        int tmp = heap[firstPos];
        heap[firstPos] = heap[secondPos];
        heap[secondPos] = tmp;
    }
}
```

### Insertion

To insert a new element, you place it at the end of the heap and then "bubble up" to its correct position.

```java
public void insert(int element) {
    if (size >= heap.length - 1) {
        // Capacity reached
        return;
    }

    // Place the new element at the end
    heap[++size] = element;
    int current = size;

    // Bubble up
    while (current > 1 && heap[current] < heap[parent(current)]) {
        swap(current, parent(current));
        current = parent(current);
    }
}
```

### Extract Min

To extract the minimum element, you remove the root and replace it with the last element in the heap. Then you "bubble down" the element to its proper position.

```java
public int extractMin() {
    int popped = heap[1];
    heap[1] = heap[size--];
    bubbleDown(1);
    return popped;
}

private void bubbleDown(int pos) {
    int smallest = pos;
    if (leftChild(pos) <= size && heap[leftChild(pos)] < heap[pos]) {
        smallest = leftChild(pos);
    }
    if (rightChild(pos) <= size && heap[rightChild(pos)] < heap[smallest]) {
        smallest = rightChild(pos);
    }
    if (smallest != pos) {
        swap(pos, smallest);
        bubbleDown(smallest);
    }
}
```

### Decrease Key

To decrease the key at a given position, you update the value and then bubble it up to its correct position.

```java
public void decreaseKey(int pos, int value) {
    heap[pos] = value;
    while (pos > 1 && heap[pos] < heap[parent(pos)]) {
        swap(pos, parent(pos));
        pos = parent(pos);
    }
}
```

### Delete

Deletion at a particular index can be done by decreasing the key value to minus infinity and then extracting the minimum.

```java
public void delete(int pos) {
    decreaseKey(pos, Integer.MIN_VALUE);
    extractMin();
}
```

### Build Heap

Building a heap from an arbitrary array can be done using the "heapify" procedure.

```java
public void buildHeap(int[] arr) {
    if (arr.length > heap.length) {
        return; // The input array is larger than the capacity of the heap
    }

    size = arr.length;
    System.arraycopy(arr, 0, heap, 1, arr.length);

    // Start heapifying from the first non-leaf node
    for (int pos = size / 2; pos >= 1; pos--) {
        bubbleDown(pos);
    }
}
```

These methods together allow you to utilize the heap in various ways. Remember that some of these operations might require a good understanding of the heap structure, so proper handling and usage are essential.
