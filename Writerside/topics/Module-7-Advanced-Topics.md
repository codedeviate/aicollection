# Module 7: Advanced Topics

## Detailed Topics:
- **Reflection**: Use reflection to inspect and manipulate objects.
    - Reflection is a powerful feature that allows programs to examine and modify their own structure and behavior at runtime. For example, you can use reflection to iterate over the fields of a struct, access private fields, or dynamically invoke methods.

  **Example:**
    ```go
    package main

    import (
        "fmt"
        "reflect"
    )

    type User struct {
        Name string
        Age  int
    }

    func main() {
        user := User{"Alice", 30}
        t := reflect.TypeOf(user)
        v := reflect.ValueOf(user)

        for i := 0; i < t.NumField(); i++ {
            fmt.Printf("Field: %s, Value: %v\n", t.Field(i).Name, v.Field(i))
        }
    }
    ```

- **JSON/XML**: Serialize and deserialize data structures.
    - JSON and XML are commonly used formats for exchanging data. In Go, you can use the `encoding/json` and `encoding/xml` packages to convert structs to these formats and back.

  **Example:**
    ```go
    package main

    import (
        "encoding/json"
        "fmt"
    )

    type User struct {
        Name string `json:"name"`
        Age  int    `json:"age"`
    }

    func main() {
        user := User{"Alice", 30}
        jsonData, _ := json.Marshal(user)
        fmt.Println(string(jsonData))

        var decodedUser User
        json.Unmarshal(jsonData, &decodedUser)
        fmt.Printf("Decoded User: %+v\n", decodedUser)
    }
    ```

- **REST APIs**: Build a web server with `net/http`.
    - Building RESTful APIs is an essential skill. Using Go’s `net/http` package, you can create endpoints for handling HTTP requests and responses.

  **Example:**
    ```go
    package main

    import (
        "encoding/json"
        "net/http"
    )

    type User struct {
        ID   int    `json:"id"`
        Name string `json:"name"`
    }

    var users = []User{
        {ID: 1, Name: "Alice"},
        {ID: 2, Name: "Bob"},
    }

    func getUsers(w http.ResponseWriter, r *http.Request) {
        w.Header().Set("Content-Type", "application/json")
        json.NewEncoder(w).Encode(users)
    }

    func main() {
        http.HandleFunc("/users", getUsers)
        http.ListenAndServe(":8080", nil)
    }
    ```

## Detailed Hands-On:

- **Create a REST API for user management:**
    - Design an API with endpoints for creating, reading, updating, and deleting users (CRUD operations).
    - Implement features like input validation and error handling.

  **Example:**
    ```go
    // Add endpoints for POST, PUT, DELETE operations in addition to GET.
    ```

- **Use JSON encoding/decoding in a data processing pipeline:**
    - Write a program that reads JSON data from a file, processes it (e.g., filtering or aggregating), and writes the output back as JSON.

  **Example:**
    ```go
    // Load users from a JSON file, filter those above a certain age, and save the results.
    ```

- **Implement reflection to dynamically handle structs:**
    - Create a function that takes an arbitrary struct and generates a JSON schema-like representation dynamically.

  **Example:**
    ```go
    func generateSchema(v interface{}) map[string]string {
        // Use reflection to produce a schema.
    }
    ```

