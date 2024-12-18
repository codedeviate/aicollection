# Module 4: Structs and Interfaces

## Detailed Topics:

### Structs:
Structs in Go are collections of fields that can represent data structures. They are used to group data together and enable the definition of methods.
- **Defining Structs**: Syntax and field definition.
  ```go
  type Person struct {
      Name string
      Age  int
  }
  ```
- **Creating and Using Structs**: Instantiating structs and accessing fields.
  ```go
  func main() {
      person := Person{Name: "Alice", Age: 30}
      fmt.Println(person.Name) // Output: Alice
  }
  ```
- **Methods on Structs**: Attaching functions to struct types.
  ```go
  func (p Person) Greet() string {
      return fmt.Sprintf("Hello, my name is %s.", p.Name)
  }
  ```
- **Struct Embedding**: Using composition to reuse fields and methods.
  ```go
  type Employee struct {
      Person
      Position string
  }
  ```

### Interfaces:
Interfaces define methods that types must implement. They enable polymorphism and decouple code.
- **Defining Interfaces**: Specifying a contract with methods.
  ```go
  type Greeter interface {
      Greet() string
  }
  ```
- **Implementing Interfaces**: Types implicitly satisfy interfaces by implementing their methods.
  ```go
  func (p Person) Greet() string {
      return fmt.Sprintf("Hi, I'm %s!", p.Name)
  }
  ```
- **Using Interfaces**: Writing functions that accept any type implementing the interface.
  ```go
  func PrintGreeting(g Greeter) {
      fmt.Println(g.Greet())
  }
  ```

## Detailed Hands-On:

### Develop an Inventory Management System Using Structs:
1. Define a `Product` struct with fields like `Name`, `Price`, and `Quantity`.
   ```go
   type Product struct {
       Name     string
       Price    float64
       Quantity int
   }
   ```
2. Add methods to calculate the total value of the stock.
   ```go
   func (p Product) TotalValue() float64 {
       return p.Price * float64(p.Quantity)
   }
   ```
3. Implement functionality to add and remove stock.
   ```go
   func (p *Product) AddStock(amount int) {
       p.Quantity += amount
   }

   func (p *Product) RemoveStock(amount int) {
       if p.Quantity >= amount {
           p.Quantity -= amount
       } else {
           fmt.Println("Not enough stock available")
       }
   }
   ```
4. Create a `Store` struct to manage multiple products and implement methods to list all products and calculate the total inventory value.
   ```go
   type Store struct {
       Products []Product
   }

   func (s Store) TotalInventoryValue() float64 {
       total := 0.0
       for _, product := range s.Products {
           total += product.TotalValue()
       }
       return total
   }
   ```

### Create a Mock Implementation Using Interfaces:
1. Define an interface `Inventory` to abstract inventory operations.
   ```go
   type Inventory interface {
       AddStock(amount int)
       RemoveStock(amount int)
       TotalValue() float64
   }
   ```
2. Implement the `Inventory` interface for the `Product` struct.
3. Write a function that works with any type implementing `Inventory`.
   ```go
   func UpdateInventory(i Inventory, add int, remove int) {
       i.AddStock(add)
       i.RemoveStock(remove)
       fmt.Printf("Updated Inventory Value: $%.2f\n", i.TotalValue())
   }
   ```
4. Test the interface with a mock struct.
   ```go
   type MockInventory struct {
       Value float64
   }

   func (m MockInventory) AddStock(amount int) {}
   func (m MockInventory) RemoveStock(amount int) {}
   func (m MockInventory) TotalValue() float64 {
       return m.Value
   }
   ```

