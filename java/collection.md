## Collection Framework

### 1. List Interface

**ArrayList**

- Implementation: Dynamic array
- Key Methods:
  - `add(E e)`: Appends the element to the end.
  - `get(int index)`=: Returns the element at the specified index.
  - `remove(int index)`: Removes the element at the specified index.
  - `size()`: Returns the number of elements.

```java
List<String> list = new ArrayList<>();
list.add("Apple");
list.add("Orange");
list.add("Banana");

// Iterate using for-each
for (String fruit : list) {
    System.out.println(fruit);
}

// Retrieve based on index
String firstFruit = list.get(0); // Apple

// Remove an element
list.remove(1); // Removes "Orange"
```

**LinkedList**

- Implementation: Doubly-linked list
- Key Methods:
  - `addFirst(E e)`: Inserts the element at the beginning.
  - `addLast(E e)`: Appends the element to the end.
  - `getFirst()`: Retrieves the first element.
  - `getLast()`: Retrieves the last element.

```java
List<String> linkedList = new LinkedList<>();
linkedList.add("Lion");
linkedList.add("Tiger");
linkedList.add("Leopard");

// LinkedList specific method
((LinkedList<String>) linkedList).addFirst("Cheetah");
```

### 2. Set Interface

**HashSet**

- Implementation: Hash table
- Key Methods:
  - `add(E e)`: Adds the specified element.
  - `contains(Object o)`: Returns true if this set contains the specified element.
  - `remove(Object o)`: Removes the specified element.

```java
Set<String> hashSet = new HashSet<>();
hashSet.add("Dog");
hashSet.add("Cat");
hashSet.add("Dog"); // Duplicate, won't be added

// Iterate
for (String animal : hashSet) {
    System.out.println(animal);
}
```

**LinkedHashSet**

```java
Set<String> linkedHashSet = new LinkedHashSet<>();
linkedHashSet.add("Dog");
linkedHashSet.add("Cat");
linkedHashSet.add("Dog"); // Duplicate, won't be added
```

**TreeSet**

```java
Set<String> treeSet = new TreeSet<>();
treeSet.add("Eagle");
treeSet.add("Falcon");
treeSet.add("Hawk");

// Retrieve first and last elements
String firstBird = treeSet.first(); // Eagle
String lastBird = treeSet.last(); // Hawk
```

### 3. Map Interface

**HashMap**

- Implementation: Hash table
- Key Methods:
  - `put(K key, V value)`: Associates the specified value with the specified key.
  - `get(Object key)`: Returns the value to which the specified key is mapped.
  - `remove(Object key)`: Removes the mapping for the specified key.
  - `containsKey(Object key)`: Returns true if this map contains a mapping for the specified key.

```java
Map<Integer, String> hashMap = new HashMap<>();
hashMap.put(1, "One");
hashMap.put(2, "Two");

// Iterate over key-values
for (Map.Entry<Integer, String> entry : hashMap.entrySet()) {
    System.out.println(entry.getKey() + ": " + entry.getValue());
}

// Retrieve value based on key
String value = hashMap.get(1); // One
```

**LinkedHashMap and TreeMap** have similar methods to `HashMap`.

### 4. Queue Interface

```java
Queue<String> queue = new LinkedList<>();
queue.add("First");
queue.add("Second");
queue.add("Third");

String head = queue.peek(); // Retrieve but don't remove head, "First"
head = queue.poll(); // Retrieve and remove head, "First"
```

### 5. Deque Interface (Double-ended queue, Stack)

- `addFirst(E e)`: Inserts the specified element at the front of this deque.
- `addLast(E e)`: Inserts the specified element at the end of this deque.
- `removeFirst()`: Retrieves and removes the first element of this deque.
- `removeLast()`: Retrieves and removes the last element of this deque.

```java
Deque<String> deque = new ArrayDeque<>();
deque.addFirst("Front");
deque.addLast("Back");
String front = deque.removeFirst();
String back = deque.removeLast();
// Deque can also be used as a Stack
Deque<String> stack = new ArrayDeque<>();
stack.push("Bottom");
stack.push("Middle");
stack.push("Top");
String top = stack.pop(); // returns "Top" and removes it
String middle = stack.peek(); // returns "Middle" without removing it
```

### 6. PriorityQueue Class

- Implementation: Heap
- Key Methods:
  - `add(E e)`: Inserts the specified element.
  - `poll()`: Retrieves and removes the head of this queue.
  - `peek()`: Retrieves, but does not remove, the head of this queue.

```java
PriorityQueue<Integer> pq = new PriorityQueue<>();
pq.add(5);
pq.add(1);
pq.add(3);
pq.add(2);
while (!pq.isEmpty()) {
    System.out.println(pq.poll());
}
```

- By default, the elements are ordered in their natural order. To use a custom order, use a custom comparator.

```java
PriorityQueue<Integer> pq = new PriorityQueue<>(Collections.reverseOrder());
```

### 7. Iterator Interface

```java
List<String> items = new ArrayList<>(Arrays.asList("A", "B", "C"));
Iterator<String> iterator = items.iterator();
while (iterator.hasNext()) {
    System.out.println(iterator.next());
}
```

### 8. Collections Class

```java
List<String> fruits = new ArrayList<>(Arrays.asList("Mango", "Peach", "Berry"));
Collections.sort(fruits); // Natural order

// Custom sorting using Comparator
Collections.sort(fruits, (a, b) -> b.compareTo(a)); // Reverse order
// other way for reversion
// Collections.sort(numbers, Collections.reverseOrder());
// Collections.sort(numbers, (a, b) -> b - a);
```

### 9. Arrays Class

```java
int[] numbers = {3, 2, 1};
Arrays.sort(numbers);
int index = Arrays.binarySearch(numbers, 2);
```
