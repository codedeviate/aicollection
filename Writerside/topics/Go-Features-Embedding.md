# Embedding

In Go, **embedding** is a mechanism that allows you to include one type (usually a struct) within another struct or interface without explicitly declaring fields or methods. Unlike traditional inheritance, embedding in Go does not imply an “is a” relationship but rather a “has a” or “contains” relationship. This design offers code reuse, method promotion, and simpler composition patterns.

Below is an in-depth look at how embedding works in Go, with several examples demonstrating its usage and behavior.

---

## 1. Struct Embedding

### 1.1 Basic Struct Embedding

When you embed one struct (say `Embedded`) inside another struct (say `Outer`), all exported fields and methods of `Embedded` become “promoted” and accessible via `Outer`.

```go
package main

import "fmt"

type Person struct {
    Name string
    Age  int
}

type Employee struct {
    Person  // Embedded struct
    ID      int
    Company string
}

func main() {
    e := Employee{
        Person: Person{
            Name: "Alice",
            Age:  30,
        },
        ID:      1001,
        Company: "TechCorp",
    }

    // Accessing fields directly
    fmt.Println("Name:", e.Name)       // promoted from Person
    fmt.Println("Age:", e.Age)         // promoted from Person
    fmt.Println("ID:", e.ID)
    fmt.Println("Company:", e.Company)
}
```

**Explanation**:
- `Employee` embeds `Person`.
- We can access `Name` and `Age` directly on `Employee` because they are promoted fields from the embedded `Person`.
- Embedding is not inheritance; it's more like `Employee` **has a** `Person`.

**Output**:
```
Name: Alice
Age: 30
ID: 1001
Company: TechCorp
```

---

### 1.2 Methods Promotion

When you embed a struct, all its exported methods are also promoted. You can call these methods on the embedding struct directly.

```go
package main

import "fmt"

type Person struct {
    Name string
}

// Method on Person
func (p Person) Greet() {
    fmt.Printf("Hello, my name is %s\n", p.Name)
}

type Employee struct {
    Person
    Company string
}

func main() {
    e := Employee{
        Person: Person{Name: "Bob"},
        Company: "InnoTech",
    }

    // Directly calling the method from the embedded struct
    e.Greet()
}
```

**Explanation**:
- `Greet()` is defined on `Person`, but by embedding `Person` in `Employee`, `Employee` also has `Greet()`.
- This is called **method promotion**.

**Output**:
```
Hello, my name is Bob
```

---

## 2. Pointer vs Value Receivers and Embedding

If you have a method that uses a pointer receiver in the embedded type, you can call it through the embedding struct whether or not the embedding struct is a value or a pointer. Go automatically adjusts the receiver appropriately.

```go
package main

import "fmt"

type Person struct {
    Name string
}

// Pointer receiver
func (p *Person) SetName(newName string) {
    p.Name = newName
}

type Employee struct {
    Person
    ID int
}

func main() {
    // e is a value
    e := Employee{
        Person: Person{Name: "Charlie"},
        ID:     42,
    }

    // Even though e is not a pointer, we can still call SetName,
    // and Go will take the address of e.Person automatically.
    e.SetName("Charlotte")
    fmt.Println("Employee Name:", e.Name)

    // If we have a pointer, it works similarly
    ep := &Employee{
        Person: Person{Name: "Dave"},
        ID:     100,
    }
    ep.SetName("David")
    fmt.Println("Employee Pointer Name:", ep.Name)
}
```

**Explanation**:
- `(*Person).SetName` is a pointer-receiver method.
- When called on `e`, which is a value, Go automatically uses `&e.Person`.
- This makes it easier to call methods on embedded fields without worrying about pointer vs value issues (within reason).

**Output**:
```
Employee Name: Charlotte
Employee Pointer Name: David
```

---

## 3. Overlapping or Shadowing Fields

If both the embedded type and the embedding type have fields of the same name, the embedding type’s field takes precedence, and you can still access the embedded type’s field with a qualified name.

```go
package main

import "fmt"

type Person struct {
    Name string
}

type Employee struct {
    Person
    Name string  // Shadowing Person.Name
}

func main() {
    e := Employee{
        Person: Person{Name: "Eve Person"},
        Name:   "Eve Employee",
    }

    // Accessing the shadowed fields
    fmt.Println("Employee Name:", e.Name)          // "Eve Employee"
    fmt.Println("Embedded Person Name:", e.Person.Name) // "Eve Person"
}
```

**Explanation**:
- Both `Employee` and `Person` have a field named `Name`.
- The direct `e.Name` refers to `Employee`’s `Name`.
- To access the `Person` field, we must fully qualify: `e.Person.Name`.

**Output**:
```
Employee Name: Eve Employee
Embedded Person Name: Eve Person
```

---

## 4. Nested Embedding

You can embed multiple levels of structs. If a struct is embedded in an embedded struct, fields and methods continue to promote upward as long as there are no conflicts.

```go
package main

import "fmt"

type Address struct {
    City  string
    State string
}

type Person struct {
    Name string
    Address
}

type Employee struct {
    Person
    ID int
}

func main() {
    e := Employee{
        Person: Person{
            Name: "Frank",
            Address: Address{
                City:  "Metropolis",
                State: "NY",
            },
        },
        ID: 9999,
    }

    // Access fields from nested embedding
    fmt.Println("Name:", e.Name)
    fmt.Println("City:", e.City)   // From Address
    fmt.Println("State:", e.State) // From Address
    fmt.Println("ID:", e.ID)
}
```

**Explanation**:
- `Employee` embeds `Person`, which in turn embeds `Address`.
- So, `Employee` has promoted fields from both `Person` and `Address`, such as `Name`, `City`, and `State`.

**Output**:
```
Name: Frank
City: Metropolis
State: NY
ID: 9999
```

---

## 5. Embedding in Interfaces

Go also allows embedding interfaces within other interfaces. This gives a form of “interface composition” rather than inheritance.

### Example: Composing Interfaces

```go
package main

import "fmt"

type Writer interface {
    Write(data []byte) (int, error)
}

type Closer interface {
    Close() error
}

// Embedded interface
type WriteCloser interface {
    Writer
    Closer
}

type MyWriterCloser struct{}

func (m MyWriterCloser) Write(data []byte) (int, error) {
    return len(data), nil
}

func (m MyWriterCloser) Close() error {
    return nil
}

func main() {
    var wc WriteCloser = MyWriterCloser{}
    n, err := wc.Write([]byte("Hello"))
    fmt.Println("Wrote bytes:", n, "Error:", err)

    if err := wc.Close(); err != nil {
        fmt.Println("Close error:", err)
    }
}
```

**Explanation**:
- `WriteCloser` is an interface that embeds `Writer` and `Closer`.
- Any type that implements both `Write` and `Close` automatically satisfies `WriteCloser`.
- This is not inheritance but rather a simpler way to combine interface contracts.

---

## 6. Embedded Unexported Fields

You can embed unexported fields too, often for implementing patterns like “private inheritance” or for providing shared functionality without exposing it to consumers.

```go
package main

import "fmt"

type internalData struct {
    secret string
}

// Exported type embedding an unexported field
type PublicType struct {
    internalData
}

func NewPublicType(secret string) *PublicType {
    return &PublicType{internalData{secret}}
}

func main() {
    p := NewPublicType("hidden value")
    // We can't access p.secret directly because it's inside unexported internalData
    // But we can expose methods on PublicType if we want to manipulate the data.
    fmt.Println(p) // &{{hidden value}}
}
```

**Explanation**:
- `internalData` is not exported (starts with a lowercase `i`).
- `PublicType` embeds `internalData` to store data internally without exposing it to callers.
- This pattern can help maintain encapsulation while using embedding for code reuse.

---

## 7. Summary of Key Points

1. **Composition Over Inheritance**:  
   Go uses embedding as a simpler mechanism for code reuse rather than traditional OOP inheritance.

2. **Promotion**:  
   Fields and methods of the embedded type are “promoted” to the embedding type, if they do not conflict with existing fields or methods.

3. **Shadowing**:  
   If the embedding type defines a field or method with the same name as an embedded field/method, the embedding type’s definition takes precedence, and the embedded one can be accessed via fully qualified syntax.

4. **Pointer vs Value**:  
   Whether you embed a pointer to a struct or a struct value, method calls can still be promoted. However, embedding a pointer to a struct has different lifecycle and memory implications than embedding by value.

5. **Nested Embedding**:  
   Embedding can be nested multiple levels deep. Fields continue to be promoted up the chain, as long as there are no name conflicts.

6. **Interface Embedding**:  
   Interfaces can embed other interfaces, effectively extending the interface set without classical inheritance.

---

## Conclusion

Embedding in Go is a powerful construct that supports clean composition patterns without the complexity of traditional class-based inheritance. By understanding how fields and methods are promoted, how shadowing works, and how nested embedding can simplify structures, you can create more maintainable and idiomatic Go programs. Whether embedding structs or interfaces, remember that it represents “has a” relationships rather than “is a.” This design principle aligns with Go’s emphasis on simplicity and composition, enabling expressive and clear code reuse.