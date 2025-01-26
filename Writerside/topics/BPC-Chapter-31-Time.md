# Chapter 31 - Time

Time is a crucial concept in programming and computing. It allows developers to measure durations, schedule tasks, perform operations based on time intervals, and format time for user interfaces. There are different types of time that programmers often work with, including **wall-clock time**, **elapsed time**, **system time**, and **monotonic time**. Each type serves specific purposes in various contexts.

This article will explore these types of time, their use cases, and how they can be implemented in different programming languages like Python, PHP, Go, C++, and Zig. By understanding these concepts, you’ll gain insights into how to effectively work with time in your projects.

## What Is Wall-Clock Time?

Wall-clock time refers to the actual time of day as it is read from a clock. This is the time most users are familiar with, formatted as hours, minutes, and seconds (e.g., `12:30 PM`). It is typically used for tasks such as:

- Displaying timestamps
- Logging events
- Scheduling events (e.g., meetings or reminders)

### Example Code: Retrieving Wall-Clock Time

- **Python**:
```python
from datetime import datetime

now = datetime.now()
print("Current Wall-Clock Time:", now)
```

- **PHP**:
```php
echo "Current Wall-Clock Time: " . date('Y-m-d H:i:s') . "\n";
```

- **Go**:
```go
package main

import (
	"fmt"
	"time"
)

func main() {
	now := time.Now()
	fmt.Println("Current Wall-Clock Time:", now)
}
```

- **C++**:
```cpp
#include <iostream>
#include <chrono>
#include <ctime>

int main() {
    auto now = std::chrono::system_clock::now();
    std::time_t currentTime = std::chrono::system_clock::to_time_t(now);
    std::cout << "Current Wall-Clock Time: " << std::ctime(&currentTime);
    return 0;
}
```

- **Zig**:
```zig
const std = @import("std");

pub fn main() !void {
    const time = try std.time.milliTimestamp();
    std.debug.print("Current Wall-Clock Time: {d}\n", .{time});
}
```

## What Is Elapsed Time?

Elapsed time measures the duration between two points in time. It is often used in performance measurement, where you determine how long a specific task takes to execute. Unlike wall-clock time, elapsed time is less affected by changes in system time (e.g., daylight savings).

### Example Code: Measuring Elapsed Time

- **Python**:
```python
import time

start = time.time()
# Simulated task
time.sleep(2)
end = time.time()
print("Elapsed Time:", end - start, "seconds")
```

- **PHP**:
```php
$start = microtime(true);
// Simulated task
usleep(2000000);
$end = microtime(true);
echo "Elapsed Time: " . ($end - $start) . " seconds\n";
```

- **Go**:
```go
package main

import (
	"fmt"
	"time"
)

func main() {
	start := time.Now()
	time.Sleep(2 * time.Second)
	elapsed := time.Since(start)
	fmt.Println("Elapsed Time:", elapsed.Seconds(), "seconds")
}
```

- **C++**:
```cpp
#include <iostream>
#include <chrono>
#include <thread>

int main() {
    auto start = std::chrono::high_resolution_clock::now();
    std::this_thread::sleep_for(std::chrono::seconds(2));
    auto end = std::chrono::high_resolution_clock::now();
    std::chrono::duration<double> elapsed = end - start;
    std::cout << "Elapsed Time: " << elapsed.count() << " seconds\n";
    return 0;
}
```

- **Zig**:
```zig
const std = @import("std");

pub fn main() !void {
    const start = std.time.milliTimestamp();
    std.time.sleep(std.time.ns_per_s * 2);
    const end = std.time.milliTimestamp();
    std.debug.print("Elapsed Time: {d} milliseconds\n", .{end - start});
}
```

## What Is System Time?

System time represents the time maintained by the operating system, typically counting seconds or milliseconds since a specific epoch (e.g., Unix epoch: January 1, 1970). It is used for low-level timekeeping and synchronization tasks.

### Example Code: Retrieving System Time

- **Python**:
```python
import time

system_time = time.time()
print("System Time:", system_time, "seconds since the epoch")
```

- **PHP**:
```php
echo "System Time: " . time() . " seconds since the epoch\n";
```

- **Go**:
```go
package main

import (
	"fmt"
	"time"
)

func main() {
	systemTime := time.Now().Unix()
	fmt.Println("System Time:", systemTime, "seconds since the epoch")
}
```

- **C++**:
```cpp
#include <iostream>
#include <chrono>

int main() {
    auto system_time = std::chrono::system_clock::now().time_since_epoch().count();
    std::cout << "System Time: " << system_time << " ticks since the epoch\n";
    return 0;
}
```

- **Zig**:

```zig
const std = @import("std");

pub fn main() !void {
    const system_time = std.time.milliTimestamp();
    std.debug.print("System Time: {d} milliseconds since the epoch\n", .{system_time});
}
```

## What Is Monotonic Time?

Monotonic time is a continuously increasing time value that is unaffected by changes in the system clock. It is used for measuring durations, especially in performance-critical applications.

### Example Code: Using Monotonic Time

- **Python**:

```python
import time

start = time.monotonic()
time.sleep(2)
end = time.monotonic()
print("Monotonic Time Elapsed:", end - start, "seconds")
```

- **PHP**:

```php
$start = hrtime(true);
// Simulated task
usleep(2000000);
$end = hrtime(true);
echo "Monotonic Time Elapsed: " . ($end - $start) / 1e9 . " seconds\n";
```

- **Go**:

```go
package main

import (
	"fmt"
	"time"
)

func main() {
	start := time.Now()
	time.Sleep(2 * time.Second)
	elapsed := time.Since(start)
	fmt.Println("Monotonic Time Elapsed:", elapsed.Seconds(), "seconds")
}
```

- **C++**:

```cpp
#include <iostream>
#include <chrono>
#include <thread>

int main() {
    auto start = std::chrono::steady_clock::now();
    std::this_thread::sleep_for(std::chrono::seconds(2));
    auto end = std::chrono::steady_clock::now();
    std::chrono::duration<double> elapsed = end - start;
    std::cout << "Monotonic Time Elapsed: " << elapsed.count() << " seconds\n";
    return 0;
}
```

- **Zig**:

```zig
const std = @import("std");

pub fn main() !void {
    const start = std.time.milliTimestampMonotonic();
    std.time.sleep(std.time.ns_per_s * 2);
    const end = std.time.milliTimestampMonotonic();
    std.debug.print("Monotonic Time Elapsed: {d} milliseconds\n", .{end - start});
}
```

## How to Format and Parse Time

Formatting and parsing time is essential for presenting time data in a readable format or for converting user input into usable time objects.

### Example Code: Formatting and Parsing

- **Python**:

```Python
from datetime import datetime

now = datetime.now()
formatted = now.strftime("%pct%Y-%pct%m-%pct%d %pct%H:%pct%M:%pct%S")
parsed = datetime.strptime(formatted, "%pct%Y-%pct%m-%pct%d %pct%H:%pct%M:%pct%S")
print("Formatted Time:", formatted)
print("Parsed Time:", parsed)
```

- **PHP**:
```php
$now = new DateTime();
$formatted = $now->format('Y-m-d H:i:s');
$parsed = DateTime::createFromFormat('Y-m-d H:i:s', $formatted);
echo "Formatted Time: $formatted\n";
echo "Parsed Time: " . $parsed->format('Y-m-d H:i:s') . "\n";
```

- **Go**:
```go
package main

import (
	"fmt"
	"time"
)

func main() {
	now := time.Now()
	formatted := now.Format("2006-01-02 15:04:05")
	parsed, _ := time.Parse("2006-01-02 15:04:05", formatted)
	fmt.Println("Formatted Time:", formatted)
	fmt.Println("Parsed Time:", parsed)
}
```

- **C++**:

```cpp
#include <iostream>
#include <iomanip>
#include <sstream>
#include <ctime>

int main() {
    std::time_t now = std::time(nullptr);
    std::stringstream ss;
    ss << std::put_time(std::localtime(&now), "%pct%Y-%pct%m-%pct%d %pct%H:%pct%M:%pct%S");
    std::string formatted = ss.str();

    std::cout << "Formatted Time: " << formatted << "\n";
    // Parsing is complex in C++, often using libraries
    return 0;
}
```

- **Zig**:
```zig
const std = @import("std");

pub fn main() !void {
    const timestamp = try std.time.milliTimestamp();
    const formatted = try std.fmt.format("{d}", .{timestamp});
    std.debug.print("Formatted Time: {s}\n", .{formatted});
}
```

## Conclusion

Understanding the different types of time in programming is essential for working with scheduling, measuring durations, and formatting or parsing time data. Each type—wall-clock time, elapsed time, system time, and monotonic time—has its unique applications and implementation considerations. By mastering time-handling techniques in various programming languages, you’ll be better equipped to handle real-world programming challenges.