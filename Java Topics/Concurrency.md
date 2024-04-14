# Java Concurrency and MultiThreading - Basics

## Contents

1. [Create Threads](#1-create-threads)
2. [Thread Names](#2-thread-names)
3. [Executors and ExecutorService](#3-executors-and-executorservice)
4. [Runnable and Callable](#4-runnable-and-callable)
5. [Mutex and Semaphore](#5-mutex-and-semaphore)

The main stage is set by the **primary thread**, launched by the Java Virtual Machine (JVM) when your application begins its performance.

## 1. Create Threads

Java threads, akin to any other Java objects, are instances of java.lang.Thread or its subclasses.

Let's dive into the nuances of creating and starting threads with a detailed exploration.
Broadly, there are two ways to specify what code the thread should execute.

- Create a subclass of `Thread` and override the `run()` method
- Pass an object that implements `Runnable` (`java.lang.Runnable`) to the `Thread` constructor

### 1.1. Thread Subclass Implementation

The classic approach involves extending the Thread class and overriding the run() method. For instance:

```java
// ThreadExample1.java
package com.sthmishra.concurrency;

public class ThreadExample1 {
    public static class MyThread extends Thread {
        @Override
        public void run() {
            System.out.println("MyThread running");
            System.out.println("MyThread finished");
        }
    }

    public static void main(String[] args) {
        MyThread myThreadObj = new MyThread();
        myThreadObj.start();
    }
}
```

### 1.2. Runnable Interface Implementation

The `Runnable` interface is a standard **Java Interface** that comes with the Java platform.
The `Runnable` interface only has a single method `run()`.

Whatever the thread is supposed to do when it executes must be included in the implementation of the `run()` method. There are three ways to implement the `Runnable` interface:

- Create a Java class that implements the `Runnable` interface.
- Create an anonymous class that implements the `Runnable` interface.
- Create a Java Lambda that implements the `Runnable` interface.

#### 1.2.1. Java Class Implements Runnable

```java
// ThreadExample2.java
package com.sthmishra.concurrency;

public class ThreadExample2 {
    public static class MyRunnableThread implements Runnable {
        @Override
        public void run() {
            System.out.println("MyRunnableThread running");
            System.out.println("MyRunnableThread finished");
        }
    }

    public static void main(String[] args) {
        MyRunnableThread myThreadObj = new MyRunnableThread();

        Thread thread = new Thread(myThreadObj);
        thread.start();
    }
}
```

#### 1.2.2. Anonymous Implementation of Runnable

```java
// ThreadExample3.java
package com.sthmishra.concurrency;

public class ThreadExample3 {
    public static void main(String[] args) {
        Runnable myRunnable = new Runnable() {
            @Override
            public void run() {
                System.out.println("MyAnonRunnableThread running");
                System.out.println("MyAnonRunnableThread finished");
            }
        };

        Thread thread = new Thread(myRunnable);
        thread.start();
    }
}
```

**Note:** Anonymous implementation is now considered to be outdated, and it is suggested to use Java Lambdas if you're not writing a separate class while implementing the `Runnable` interface. However, please keep in mind that if your `Runnable` implementation needs more than just the `run()` method (e.g. a `stop()` or `pause()` method too), then you can no longer create your `Runnable` implementation with a Java lambda expression. A Java lambda can only implement a single method. Instead, you must use a custom class, or a custom interface that extends `Runnable` which has the extra methods, and which is implemented by an anonymous class.

#### 1.2.3. Java Lambda Implementation of Runnable

```java
// ThreadExample4.java
package com.sthmishra.concurrency;

public class ThreadExample4 {
    public static void main(String[] args) {
        Runnable myRunnable = () -> {
            System.out.println("Lambda running");
            System.out.println("Lambda finished");
        };

        Thread thread = new Thread(myRunnable);
        thread.start();
    }
}
```

### 1.3. Choosing Between Subclassing and Implementing Runnable

The choice between extending Thread or implementing Runnable depends on one's design preferences. However, implementing `Runnable` is a more popular choice for most developers.

When having the `Runnable`'s executed by a **thread pool** it is easy to queue up the `Runnable` instances until a thread from the pool is idle. This is a little harder to do with `Thread` subclasses.

## 2. Thread Names

When you create a Java thread you can give it a name. The name can help you distinguish different threads from each other. For instance, if multiple threads write to the console it can be handy to see which thread wrote the text. Here is an example:

```java
// ThreadReference.java
package com.sthmishra.concurrency;

public class ThreadReference {
    public static class MyRunnable implements Runnable {
        @Override
        public void run() {
            String threadName = Thread.currentThread().getName(); // fetch our new thread's name
            System.out.println(threadName + " running");
        }
    }

    public static void main(String[] args) {
        MyRunnable obj = new MyRunnable();

        // fetch the name of the current running thread, i.e., the main thread by JVM
        System.out.println(Thread.currentThread().getName() + " running in main method");

        Thread thread = new Thread(obj, "MyRunnableMod"); // pass in the name of the thread
        thread.start();
    }
}
```

Output:

```
main running in main method
MyRunnableMod running
```

## 3. Executors and ExecutorService

The `Executors` class and the `ExecutorService` interface provide a framework for managing
and controlling the execution of concurrent tasks using a pool of worker threads.

These components are part of the `java.util.concurrent package`, which
offers a higher-level concurrency framework compared to traditional
thread-based approaches.

### 3.1. newFixedThreadPool and newCachedThreadPool

`ExecutorService.newFixedThreadPool` and `ExecutorService.newCachedThreadPool` are
two methods provided by the `ExecutorService` interface in Java to
create thread pools with different characteristics.

#### 3.1.1. `newFixedThreadPool(int nThreads)` method:

- **Description:** This method creates a fixed-size thread pool where the number of threads
  remains constant. The pool has a specified number of threads (nThreads)
  that are all active and available for executing tasks.
  If a task is submitted when all threads are busy,
  it is queued until a thread becomes available.
  If a thread encounters an exception and terminates, a new one will be created to
  replace it.

- **Use Case:** Suitable for scenarios where a fixed number of threads
  is desired to control resource usage, especially when tasks
  may have dependencies and need to be executed concurrently
  with a controlled degree of parallelism.

```java
// FixedThreadPoolExample.java
package com.sthmishra.concurrency;

import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class FixedThreadPoolExample {
    public static void main(String[] args) {
        ExecutorService fixedThreadPool = Executors.newFixedThreadPool(10);

        for(int i = 0; i < 100; i++) {
            int taskId = i+1;
            Runnable runnable = () -> {
                String currentThreadName = Thread.currentThread().getName();
                System.out.println("Task " + taskId + " executed by thread " + currentThreadName);
            };
            fixedThreadPool.execute(runnable);
        }

        fixedThreadPool.shutdown();
    }
}
```

#### 3.1.2. `newCachedThreadPool()` method:

- **Description:** This method creates a thread pool that dynamically
  adjusts its size based on the number of active tasks.
  Threads are created on-demand and reused if available, otherwise, a new thread is created.
  Threads that have been idle for a certain period may be terminated
  and removed from the pool to conserve resources.

- **Use Case:** Suitable for scenarios with a variable number of tasks
  and where threads can be created and terminated as needed.
  It's a good choice for handling a large number of short-lived asynchronous tasks.

```java
// CachedThreadPoolExample.java
package com.sthmishra.concurrency;

import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class CachedThreadPoolExample {
    public static void main(String[] args) {
        ExecutorService cachedThreadPool = Executors.newCachedThreadPool();

        for(int i = 0; i < 100; i++) {
            int taskId = i+1;
            Runnable runnable = () -> {
                String currentThreadName = Thread.currentThread().getName();
                System.out.println("Task " + taskId + " executed by thread " + currentThreadName);
            };
            cachedThreadPool.execute(runnable);
        }

        cachedThreadPool.shutdown();
    }
}
```

## 4. Runnable and Callable

Both `Runnable` and `Callable` are interfaces that represent a task that can be executed concurrently. However, they differ in the following ways -

- The `Runnable` interface has a single `run()` method that does not return a value.
- The `Callable` interface has a single `call()` method that returns a result of a specified type and can throw a checked exception.

- We use the `execute` method of `ExecutorService` to pass in a runnable object.
- We use the `submit` method of `ExecutorService` to pass in a callable object. This returns a `Future<T>` object and we use the `get()` method of the future to store the final result.

- In the above examples of thread pools, we have shown how to use Runnable instances. Here is a famous example of performing concurrent merge sort using callables.

```java
public class Sorter implements Callable<List<Integer>> {
    private List<Integer> arrayToSort;
    private ExecutorService es;

    Sorter(List<Integer> arr, ExecutorService es) {
        this.arrayToSort = arr;
        this.es = es;
    }

    @Override
    public List<Integer> call() throws Exception {
        if(arrayToSort.size() <= 1) {
            return arrayToSort;
        }

        int size = arrayToSort.size();
        int mid = size/2;

        List<Integer> leftArr = new ArrayList<>();
        List<Integer> rightArr = new ArrayList<>();

        for(int i = 0;  i < mid; i++) {
            leftArr.add(arrayToSort.get(i));
        }

        for(int i = mid; i < size; i++) {
            rightArr.add(arrayToSort.get(i));
        }

        Sorter leftArraySorter = new Sorter(leftArr, es);
        Sorter rightArraySorter = new Sorter(rightArr, es);

        Future<List<Integer>> LeftSortedArrayFuture = es.submit(leftArraySorter);
        Future<List<Integer>> RightSortedArrayFuture = es.submit(rightArraySorter);

        List<Integer> leftSortedArr = LeftSortedArrayFuture.get();
        List<Integer> rightSortedArr = RightSortedArrayFuture.get();

        int i = 0;
        int j = 0;

        List<Integer> sortedArr = new ArrayList<>();

        while(i < leftSortedArr.size() && j < rightSortedArr.size()) {
            if(leftSortedArr.get(i) <= rightSortedArr.get(j)) {
                sortedArr.add(leftSortedArr.get(i++));
            } else {
                sortedArr.add(rightSortedArr.get(j++));
            }
        }

        while(i < leftSortedArr.size()) {
            sortedArr.add(leftSortedArr.get(i++));
        }

        while(j < rightSortedArr.size()) {
            sortedArr.add(rightSortedArr.get(j++));
        }

        return sortedArr;
    }
}
```

**Client Code**

```java
public class Client {
    public static void main(String[] args) {
        List<Integer> arr = Arrays.asList(8, 1, 6, 2, 3, 9, 7, 5);
        ExecutorService es = Executors.newCachedThreadPool();

        Future<List<Integer>> resultFuture = es.submit(new Sorter(arr, es));
        List<Integer> result = new ArrayList<>();

        try {
            result = resultFuture.get();
        }
        catch(Exception e) {
            System.out.println(e.getMessage());
        }

        System.out.println(result.toString());
    }
}
```

## 5. Mutex and Semaphore

### 5.1. Mutex

A mutex (is derived from _mutual exclusion_) or lock is a special mecahnism for synchronizing threads. One is "attached" to every object in Java — it doesn't matter if you use standard classes or create your own classes, e.g. Cat and Dog: **all objects of all classes have a mutex**.

This is achieved via the `synchronized` keyword.

```java
public class MutexExample {
    private static int counter = 0;

    public static synchronized void increment() {
        counter++;
    }

    public static void main(String[] args) {
        Thread thread1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                increment();
            }
        });

        Thread thread2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                increment();
            }
        });

        thread1.start();
        thread2.start();

        try {
            thread1.join();
            thread2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println("Counter: " + counter);
    }
}
```

Another famous use case of mutex is the thread-safe implementation of the Singleton design pattern.

### 5.2. Semaphore

Semaphore is a synchronization mechanism that can be used to control access to a shared resource by limiting the number of threads that can access the resource concurrently.

```java
public class ConcurrentTask implements Runnable {
    private Semaphore semaphore;
    private int id;

    ConcurrentTask(Semaphore semaphore, int id) {
        this.semaphore = semaphore;
        this.id = id;
    }

    @Override
    public void run() {
        try {
            semaphore.acquire(); // allow only 2 threads
            System.out.println("Thread " + Thread.currentThread().getName() + " started work on task " + id + "...");
            // simulating work
            Thread.sleep(2000);
            System.out.println("Thread " + Thread.currentThread().getName() + " finished work on task " + id);
        }
        catch(InterruptedException e) {
            System.out.println("Oops!");
            System.out.println(e.getMessage());
        }
        finally {
            semaphore.release();
        }
    }
}
```

**Client Code**

```java
public class Client {
    public static void main(String[] args) {
        ExecutorService es = Executors.newFixedThreadPool(20);
        Semaphore semaphore = new Semaphore(2);

        for(int i = 1; i <= 10; i++) {
            ConcurrentTask task = new ConcurrentTask(semaphore, i);
            es.execute(task);
        }

        es.shutdown();
    }
}
```
