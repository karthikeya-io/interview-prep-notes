## Heap Problems

Common heap-based DSA interview problems, with questions, hints, and solutions:

---

### 1. Kth Largest Element in an Array

**Problem**: Given an integer array, find the kth largest element.

**Hint**: A min-heap of size k can be used to solve this problem in O(n log k) time.

**Solution**:

```java
import java.util.PriorityQueue;

public int findKthLargest(int[] nums, int k) {
    // Use a min-heap of size k
    PriorityQueue<Integer> heap = new PriorityQueue<>();
    for (int num : nums) {
        heap.offer(num);
        if (heap.size() > k) {
            heap.poll();
        }
    }
    return heap.peek();
}
```

**Time Complexity**: O(n log k)

---

### 2. Merge k Sorted Lists

**Problem**: You are given an array of k linked-lists, each linked-list is sorted in ascending order. Merge all the linked-lists into one sorted linked-list.

**Hint**: Use a min-heap to compare the first node of each list. The heap should be of size k. This problem can be solved in O(N log k) time where N is the total number of nodes.

**Solution**:

Definition for singly-linked list:

```java
public class ListNode {
    int val;
    ListNode next;
    ListNode() {}
    ListNode(int val) { this.val = val; }
    ListNode(int val, ListNode next) { this.val = val; this.next = next; }
}
```

Solution:

```java
import java.util.PriorityQueue;

public ListNode mergeKLists(ListNode[] lists) {
    PriorityQueue<ListNode> heap = new PriorityQueue<>(Comparator.comparingInt(a -> a.val));

    // Initialize the heap with the first node from each list
    for (ListNode list : lists) {
        if (list != null) {
            heap.offer(list);
        }
    }

    ListNode dummy = new ListNode(0);
    ListNode tail = dummy;

    while (!heap.isEmpty()) {
        ListNode curr = heap.poll();
        tail.next = curr;
        tail = tail.next;

        if (curr.next != null) {
            heap.offer(curr.next);
        }
    }

    return dummy.next;
}
```

**Time Complexity**: O(N log k)

---

### 3. Find Median from Data Stream

**Problem**: Design a data structure that supports adding numbers and finding the current median.

**Hint**: Use two heaps, a max-heap to represent numbers below the median, and a min-heap for numbers above the median. The median is either the top of the max-heap or an average of the top of both heaps, depending on the number of elements.

**Solution**:

```java
import java.util.PriorityQueue;

public class MedianFinder {
    PriorityQueue<Integer> lo; // Max-heap
    PriorityQueue<Integer> hi; // Min-heap

    public MedianFinder() {
        lo = new PriorityQueue<>(Comparator.reverseOrder());
        hi = new PriorityQueue<>();
    }

    public void addNum(int num) {
        lo.offer(num);
        hi.offer(lo.poll());

        if (lo.size() < hi.size()) {
            lo.offer(hi.poll());
        }
    }

    public double findMedian() {
        if (lo.size() > hi.size()) {
            return lo.peek();
        } else {
            return (lo.peek() + hi.peek()) * 0.5;
        }
    }
}
```

**Time Complexity**: O(log n) for `addNum`, O(1) for `findMedian`.

---

### 4. Sliding Window Maximum

**Problem**: Given an array and an integer k, find the maximum for each and every contiguous subarray of size k.

**Hint**: A variation of heap called a double-ended queue (Deque) can be used for this, but a max-heap can also be used to track the maximum in the current window.

**Solution**:

```java
import java.util.Deque;
import java.util.LinkedList;

public int[] maxSlidingWindow(int[] nums, int k) {
    if (nums == null || k <= 0) {
        return new int[0];
    }

    int n = nums.length;
    int[] result = new int[n - k + 1];
    int ri = 0;

    // Use a deque to store indices
    Deque<Integer> deque = new LinkedList<>();

    for (int i = 0; i < nums.length; i++) {
        // Remove numbers out of range k from the front
        while (!deque.isEmpty() && deque.peek() < i - k + 1) {
            deque.poll();
        }

        // Remove smaller numbers as they're useless
        while (!deque.isEmpty() && nums[deque.peekLast()] < nums[i]) {
            deque.pollLast();
        }

        // Offer current number
        deque.offer(i);
        if (i >= k - 1) {
            result[ri++] = nums[deque.peek()];
        }
    }

    return result;
}
```

**Time Complexity**: O(n)

---

### 5. Top K Frequent Elements

**Problem**: Given a non-empty array of integers, return the k most frequent elements.

**Hint**: Create a frequency map for all elements in the array. Then, use a min-heap to track the top k frequent numbers.

**Solution**:

```java
import java.util.*;

public List<Integer> topKFrequent(int[] nums, int k) {
    Map<Integer, Integer> frequencyMap = new HashMap<>();
    for (int num : nums) {
        frequencyMap.put(num, frequencyMap.getOrDefault(num, 0) + 1);
    }

    // Min-heap
    PriorityQueue<Integer> heap = new PriorityQueue<>(Comparator.comparingInt(frequencyMap::get));
    for (int key : frequencyMap.keySet()) {
        heap.offer(key);
        if (heap.size() > k) {
            heap.poll();
        }
    }

    List<Integer> topK = new LinkedList<>();
    while (!heap.isEmpty()) {
        topK.add(heap.poll());
    }

    Collections.reverse(topK); // For the descending order
    return topK;
}
```

**Time Complexity**: O(n log k)

---

These are the top 5 heap-based problems with hints and their respective solutions. Remember, understanding the hints and deriving the solutions on your own is crucial for success in interviews!
