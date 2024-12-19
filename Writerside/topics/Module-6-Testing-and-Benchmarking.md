# Module 6: Testing and Benchmarking

## Detailed Topics:

### Unit Testing
Unit testing is the process of writing tests to verify that individual units of code (e.g., functions or methods) behave as expected. Unit tests in Go can be written using the built-in `testing` package.

#### Key Points (1):
- Unit tests are functions with names starting with `Test`, e.g., `TestAdd`.
- Use `t.Error` or `t.Errorf` to report test failures.
- Organize tests in a `_test.go` file.

#### Example (1):
```go
// calculator.go
package calculator

func Add(a, b int) int {
    return a + b
}
```

```go
// calculator_test.go
package calculator

import "testing"

func TestAdd(t *testing.T) {
    result := Add(2, 3)
    expected := 5
    if result != expected {
        t.Errorf("Add(2, 3) = %d; want %d", result, expected)
    }
}
```

### Table-Driven Tests
Table-driven tests use a table (a slice of structs) to organize test inputs and expected outputs. This approach simplifies managing multiple test cases.

#### Key Points (2):
- Useful for functions with multiple test cases.
- Improves readability and reduces code duplication.

#### Example (2):
```go
func TestAddTableDriven(t *testing.T) {
    tests := []struct {
        name     string
        a, b     int
        expected int
    }{
        {"positive numbers", 2, 3, 5},
        {"negative numbers", -2, -3, -5},
        {"mixed numbers", -2, 3, 1},
    }

    for _, tt := range tests {
        t.Run(tt.name, func(t *testing.T) {
            result := Add(tt.a, tt.b)
            if result != tt.expected {
                t.Errorf("Add(%d, %d) = %d; want %d", tt.a, tt.b, result, tt.expected)
            }
        })
    }
}
```

### Benchmarking
Benchmarking measures the performance of your code. Go provides support for benchmarking via the `testing` package with functions prefixed by `Benchmark`.

#### Key Points (3):
- Benchmarks use `b *testing.B` as an argument.
- Use `b.N` to control the number of iterations.
- Focus on optimizing code based on benchmark results.

#### Example (3):
```go
func BenchmarkAdd(b *testing.B) {
    for i := 0; i < b.N; i++ {
        Add(2, 3)
    }
}
```

## Detailed Hands-On

### 1. Write and Run Unit Tests for a Calculator Package
1. Create a `calculator` package with functions `Add`, `Subtract`, `Multiply`, and `Divide`.
2. Write unit tests for each function, using both standard and table-driven approaches.
3. Run tests using:
   ```bash
   go test ./...
   ```
4. Verify all tests pass.

#### Example (4):
```go
func Subtract(a, b int) int {
    return a - b
}

func TestSubtract(t *testing.T) {
    tests := []struct {
        a, b     int
        expected int
    }{
        {5, 3, 2},
        {2, 3, -1},
        {0, 0, 0},
    }

    for _, tt := range tests {
        t.Run("TestSubtract", func(t *testing.T) {
            result := Subtract(tt.a, tt.b)
            if result != tt.expected {
                t.Errorf("Subtract(%d, %d) = %d; want %d", tt.a, tt.b, result, tt.expected)
            }
        })
    }
}
```

### 2. Benchmark Sorting Algorithms and Optimize Performance
1. Implement different sorting algorithms (e.g., Bubble Sort, Merge Sort).
2. Write benchmarks for each algorithm.
3. Analyze the benchmark results and optimize the slower algorithms.
4. Run benchmarks using:
   ```bash
   go test -bench .
   ```

#### Example (5):
```go
func BubbleSort(arr []int) {
    n := len(arr)
    for i := 0; i < n-1; i++ {
        for j := 0; j < n-i-1; j++ {
            if arr[j] > arr[j+1] {
                arr[j], arr[j+1] = arr[j+1], arr[j]
            }
        }
    }
}

func BenchmarkBubbleSort(b *testing.B) {
    arr := []int{5, 3, 8, 4, 2}
    for i := 0; i < b.N; i++ {
        BubbleSort(arr)
    }
}
```

By completing these exercises, you will gain practical experience in writing robust tests and analyzing code performance.

