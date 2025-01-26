# Chapter 25c - Mutex

In modern programming, one common challenge is ensuring that multiple threads or processes access shared resources in a safe and consistent manner. This is where **mutexes** come into play. A mutex, short for "mutual exclusion," is a synchronization primitive that allows only one thread or process to access a shared resource at a time. Mutexes are essential in multithreading and concurrent programming to avoid race conditions and ensure data consistency.

Mutexes come in various types, each tailored to specific use cases. The main types of mutexes include:

1. **Simple Mutex**: A basic lock mechanism where one thread acquires the lock and others must wait until it is released.
2. **Recursive Mutex**: Allows a thread that has already acquired the lock to lock it again without causing a deadlock. Useful for reentrant functions.
3. **Timed Mutex**: Provides a timeout mechanism, allowing threads to wait for a specified duration to acquire the lock.
4. **Shared Mutex**: Enables multiple threads to read a resource simultaneously while allowing only one thread to write.
5. **Spinlock**: A lightweight mutex that continuously checks for the lock's availability, useful for short critical sections.

Below, we’ll explore each type, when to use them, and examples in Python, PHP, Go, C++, and Zig.

---

## The Basics of Simple Mutexes

A **simple mutex** ensures mutual exclusion by allowing only one thread to acquire the lock at a time. If a second thread tries to acquire the lock, it will block until the first thread releases it. Simple mutexes are suitable for protecting critical sections where shared resources are accessed.

### Example Code for Simple Mutex
**Python (using `threading`):**
```python
import threading

mutex = threading.Lock()

def critical_section():
    with mutex:
        print("Critical section accessed by", threading.current_thread().name)

thread1 = threading.Thread(target=critical_section)
thread2 = threading.Thread(target=critical_section)

thread1.start()
thread2.start()

thread1.join()
thread2.join()
```

**PHP (using `synchronized` in pthreads):**
```php
class SharedResource extends Threaded {
    public function criticalSection() {
        $this->synchronized(function() {
            echo "Critical section accessed by thread\n";
        });
    }
}

$resource = new SharedResource();
$thread1 = new Thread(function() use ($resource) {
    $resource->criticalSection();
});
$thread2 = new Thread(function() use ($resource) {
    $resource->criticalSection();
});

$thread1->start();
$thread2->start();

$thread1->join();
$thread2->join();
```

**Go (using `sync.Mutex`):**
```go
package main

import (
    "fmt"
    "sync"
)

var mutex sync.Mutex

func criticalSection() {
    mutex.Lock()
    fmt.Println("Critical section accessed")
    mutex.Unlock()
}

func main() {
    var wg sync.WaitGroup
    wg.Add(2)

    go func() {
        defer wg.Done()
        criticalSection()
    }()

    go func() {
        defer wg.Done()
        criticalSection()
    }()

    wg.Wait()
}
```

**C++ (using `std::mutex`):**
```cpp
#include <iostream>
#include <thread>
#include <mutex>

std::mutex mtx;

void critical_section() {
    std::lock_guard<std::mutex> lock(mtx);
    std::cout << "Critical section accessed" << std::endl;
}

int main() {
    std::thread t1(critical_section);
    std::thread t2(critical_section);

    t1.join();
    t2.join();

    return 0;
}
```

**Zig (using `std.Thread`):**
```zig
const std = @import("std");

fn criticalSection() void {
    std.debug.print("Critical section accessed\n", .{});
}

pub fn main() !void {
    var lock = std.Thread.Mutex.init();
    try lock.lock();
    defer lock.unlock();

    try std.Thread.spawn(criticalSection, .{});
    criticalSection();
}
```

---

## Recursive Mutex: Handling Reentrant Code

A **recursive mutex** allows the same thread to acquire the lock multiple times without causing a deadlock. This is particularly useful for reentrant functions, where a function might call itself and attempt to reacquire the lock.

### Example Code for Recursive Mutex
**Python (using `RLock`):**
```python
import threading

mutex = threading.RLock()

def recursive_function(count):
    if count <= 0:
        return
    with mutex:
        print(f"Reentrant lock acquired: {count}")
        recursive_function(count - 1)

recursive_function(3)
```

**C++ (using `std::recursive_mutex`):**
```cpp
#include <iostream>
#include <thread>
#include <mutex>

std::recursive_mutex rmtx;

void recursive_function(int count) {
    if (count <= 0) return;

    std::lock_guard<std::recursive_mutex> lock(rmtx);
    std::cout << "Reentrant lock acquired: " << count << std::endl;
    recursive_function(count - 1);
}

int main() {
    std::thread t(recursive_function, 3);
    t.join();
    return 0;
}
```

---

## Timed Mutex: Adding Timeouts to Locks

A **timed mutex** lets a thread attempt to acquire a lock for a specified duration. This avoids indefinite blocking if a lock cannot be obtained.

### Example Code for Timed Mutex
**C++ (using `std::timed_mutex`):**
```cpp
#include <iostream>
#include <thread>
#include <mutex>
#include <chrono>

std::timed_mutex tmtx;

void try_lock_for() {
    if (tmtx.try_lock_for(std::chrono::milliseconds(500))) {
        std::cout << "Lock acquired within timeout" << std::endl;
        tmtx.unlock();
    } else {
        std::cout << "Failed to acquire lock within timeout" << std::endl;
    }
}

int main() {
    std::thread t(try_lock_for);
    t.join();
    return 0;
}
```

---

## Shared Mutex: Simultaneous Reading and Exclusive Writing

A **shared mutex** allows multiple threads to read from a resource concurrently but ensures only one thread can write at any given time. This is often used in read-heavy workloads.

### Example Code for Shared Mutex
**C++ (using `std::shared_mutex`):**
```cpp
#include <iostream>
#include <shared_mutex>
#include <thread>

std::shared_mutex smtx;

void reader() {
    std::shared_lock<std::shared_mutex> lock(smtx);
    std::cout << "Read operation" << std::endl;
}

void writer() {
    std::unique_lock<std::shared_mutex> lock(smtx);
    std::cout << "Write operation" << std::endl;
}

int main() {
    std::thread t1(reader);
    std::thread t2(writer);

    t1.join();
    t2.join();

    return 0;
}
```

---

## Spinlocks: Lightweight but Busy-Waiting Mutexes

**Spinlocks** are lightweight mutexes where a thread continuously checks for the lock’s availability in a loop. They are useful for short critical sections but waste CPU cycles during contention.

### Example Code for Spinlocks
**Go (using a custom spinlock):**
```go
package main

import (
    "fmt"
    "runtime"
    "sync/atomic"
)

type Spinlock struct {
    locked int32
}

func (s *Spinlock) Lock() {
    for !atomic.CompareAndSwapInt32(&s.locked, 0, 1) {
        runtime.Gosched()
    }
}

func (s *Spinlock) Unlock() {
    atomic.StoreInt32(&s.locked, 0)
}

func main() {
    var lock Spinlock
    lock.Lock()
    fmt.Println("Lock acquired")
    lock.Unlock()
    fmt.Println("Lock released")
}
```

---

## Choosing the Right Mutex for Your Application

Understanding the nuances of different mutex types is critical for writing efficient and safe concurrent programs. Use simple mutexes for basic scenarios, recursive mutexes for reentrant code, and shared mutexes for read-heavy workloads. Timed mutexes and spinlocks are specialized tools that can enhance performance or reliability in specific cases. By carefully selecting the appropriate mutex, you can ensure safe and efficient multithreaded applications.