**Java Concurrency**

Java Concurrency is a term that covers multithreading, concurrency and parallelism on the Java platform. It includes the concepts of multithreading, immutability, thread safety, and the java.util.concurrent package.

1. **Threads and Runnable Interface**

   Java provides built-in support for multithreaded programming. A multi-threaded program contains two or more parts that can run concurrently. Each part of such a program is called a thread, and each thread defines a separate path of execution.

   There are two ways to create a thread in Java: by extending the `Thread` class and by implementing the `Runnable` interface.

   ```java
   // By extending Thread class
   class MyThread extends Thread {
       public void run() {
           System.out.println("Thread created by extending Thread class");
       }
   }
   // By implementing Runnable interface
   class MyRunnable implements Runnable {
       public void run() {
           System.out.println("Thread created by implementing Runnable interface");
       }
   }

   public static void main(String[] args) {
       MyThread myThread = new MyThread();
       myThread.start();

       Thread thread = new Thread(new MyRunnable());
       thread.start();
   }
   ```

2. **Thread Lifecycle**

   ![Thread Lifecycle](https://www.baeldung.com/wp-content/uploads/2016/05/Thread-Lifecycle.png)

   1. **New**: A new thread begins its life cycle in the new state. It remains in this state until the program starts the thread. It is also referred to as a born thread.
   2. **Runnable**: After a newly born thread is started, the thread becomes runnable. A thread in this state is considered to be executing its task.
   3. **Waiting**: Sometimes, a thread transitions to the waiting state while the thread waits for another thread to perform a task. A thread transitions back to the runnable state only when another thread signals the waiting thread to continue executing.
   4. **Timed Waiting**: A runnable thread can enter the timed waiting state for a specified interval of time. A thread in this state transitions back to the runnable state when that time interval expires or when the event it is waiting for occurs.
   5. **Terminated**: A runnable thread enters the terminated state when it completes its task or otherwise terminates.

- Thread.sleep(): Makes the current thread to pause for a specified time.

```java
public void run() {
    for (int i = 0; i < 5; i++) {
        System.out.println(i);
        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            System.out.println(e);
        }
    }
}
```

3. **Synchronization**

   Synchronization in Java is an important concept since Java is a multi-threaded language where multiple threads run in parallel to complete program execution. In multi-threaded environment synchronization of java object or synchronization of java class becomes extremely important.
   Synchronization is mainly used to

   1. prevent thread interference,
   2. prevent consistency problem.

   ```java
   class Counter {
       private int count = 0;
       public synchronized void increment() {
           count++;
       }
       public int getCount() {
           return count;
       }
   }

   Counter counter = new Counter();

   // Create two threads that run our increment method of our counter object
   Thread thread1 = new Thread(() -> {
       for (int i = 0; i < 10000; i++) {
           counter.increment();
       }
   });

   Thread thread2 = new Thread(() -> {
       for (int i = 0; i < 10000; i++) {
           counter.increment();
       }
   });

   // Start both threads
   thread1.start();
   thread2.start();

   // Wait for both threads to finish
   thread1.join();
   thread2.join();

   // Print final result
   System.out.println(counter.getCount());
   ```

4. **Deadlock and Starvation**

   Deadlock is a programming situation where two or more threads are blocked forever, this situation arises with at least two threads and two or more resources.

   Starvation describes a situation where a thread is unable to gain regular access to shared resources and is unable to make progress. This happens when shared resources are made unavailable for long periods by "greedy" threads.

5. **The java.util.concurrent package**

   This package includes a number of additions to the Java Collections Framework and java.util that are designed to assist in the development of concurrent (multithreaded) classes.

   - Executors
   - ConcurrentHashMap
   - BlockingQueue
   - Future and Callable

   These are the new constructs added to JDK 5.

Remember, writing thread-safe code is one of the key challenges of Java programming, as improper handling can lead to various issues like data inconsistency, deadlocks, etc. Understanding and properly using the synchronization techniques and concurrent collections will help you to avoid these issues and make your code more robust and efficient.
