# Final Project: E-Commerce API Client in Go

## Introduction
For the final project of this programming course, you will develop an API client in Go for an e-commerce system. This project is designed to showcase your skills in building practical and efficient software, leveraging Go’s features for web communication, JSON handling, and robust error management. By completing this project, you will demonstrate your ability to integrate concepts learned during the course into a comprehensive application.

## Project Goals
The primary goals of this project include:
1. **Understanding API Communication**: Learn to interact with RESTful APIs, including sending requests and handling responses.
2. **JSON Data Management**: Develop skills in parsing and generating JSON data structures.
3. **Go Programming Proficiency**: Apply Go’s features such as structs, slices, and maps in a real-world scenario.
4. **Error Handling**: Implement robust error management to handle API and application errors effectively.
5. **Project Structuring**: Design a maintainable and extensible project structure.

## Requirements
Your API client will interact with an e-commerce API to perform the following operations:

1. **Fetch Products**:
    - Retrieve a list of products with optional filtering parameters.
2. **Product Details**:
    - Fetch detailed information about a specific product by its ID.
3. **Create Orders**:
    - Submit a new order containing customer information, products, and quantities.
4. **View Orders**:
    - Retrieve details of an existing order by its ID.
5. **Update Orders**:
    - Modify details of an order, such as updating its status.
6. **Delete Orders**:
    - Remove an order from the system.

## Technical Guidelines
1. **Programming Language**: Use Go as the primary programming language.
2. **HTTP Client**: Utilize Go’s `net/http` package for HTTP requests.
3. **JSON Handling**: Leverage the `encoding/json` package for JSON serialization and deserialization.
4. **Error Handling**: Implement structured error responses to handle API errors gracefully.
5. **Authentication**: Add support for API key-based authentication (e.g., Bearer tokens).
6. **Code Documentation**: Write clear comments explaining each function and its purpose.
7. **Testing**: Include unit tests to verify the functionality of critical operations.

## Suggested Project Structure
Organize your project into logical components to improve readability and maintainability:
- **main.go**: Entry point of the application.
- **api/**: Contains functions and methods for interacting with the API.
- **models/**: Defines data structures for products, orders, and other entities.
- **utils/**: Includes helper functions for tasks like JSON handling and error formatting.
- **tests/**: Contains unit tests for your API client.

## Project Files

> **Note**: The following files are examples to guide you in structuring your project. You can modify them based on your implementation and requirements.
> {style="warning"}

### main.go
```go
package main

import (
	"fmt"
	"github.com/your_username/ecommerce-client/api"
)

func main() {
	client := api.NewECommerceAPIClient("https://api.example.com", "your_api_key_here")

	// Example: Fetch products
	products, err := client.GetProducts(nil)
	if err != nil {
		fmt.Println("Error fetching products:", err)
	} else {
		fmt.Println("Products:", string(products))
	}
}
```

### api/client.go
```go
package api

import (
	"bytes"
	"encoding/json"
	"fmt"
	"io/ioutil"
	"net/http"
)

type ECommerceAPIClient struct {
	BaseURL string
	APIKey  string
}

func NewECommerceAPIClient(baseURL, apiKey string) *ECommerceAPIClient {
	return &ECommerceAPIClient{
		BaseURL: baseURL,
		APIKey:  apiKey,
	}
}

func (client *ECommerceAPIClient) makeRequest(method, endpoint string, body interface{}) ([]byte, error) {
	url := fmt.Sprintf("%pct%s%pct%s", client.BaseURL, endpoint)
	var reqBody []byte
	var err error

	if body != nil {
		reqBody, err = json.Marshal(body)
		if err != nil {
			return nil, err
		}
	}

	req, err := http.NewRequest(method, url, bytes.NewBuffer(reqBody))
	if err != nil {
		return nil, err
	}

	req.Header.Set("Authorization", fmt.Sprintf("Bearer %s", client.APIKey))
	req.Header.Set("Content-Type", "application/json")

	clientHTTP := &http.Client{}
	resp, err := clientHTTP.Do(req)
	if err != nil {
		return nil, err
	}
	defer resp.Body.Close()

	respBody, err := ioutil.ReadAll(resp.Body)
	if err != nil {
		return nil, err
	}

	if resp.StatusCode < 200 || resp.StatusCode >= 300 {
		return nil, fmt.Errorf("error: status code %d, message: %s", resp.StatusCode, string(respBody))
	}

	return respBody, nil
}

func (client *ECommerceAPIClient) GetProducts(params map[string]string) ([]byte, error) {
	endpoint := "/products"
	return client.makeRequest("GET", endpoint, nil)
}

func (client *ECommerceAPIClient) GetProductDetails(productID string) ([]byte, error) {
	endpoint := fmt.Sprintf("/products/%s", productID)
	return client.makeRequest("GET", endpoint, nil)
}

func (client *ECommerceAPIClient) CreateOrder(orderData map[string]interface{}) ([]byte, error) {
	endpoint := "/orders"
	return client.makeRequest("POST", endpoint, orderData)
}

func (client *ECommerceAPIClient) GetOrderDetails(orderID string) ([]byte, error) {
	endpoint := fmt.Sprintf("/orders/%s", orderID)
	return client.makeRequest("GET", endpoint, nil)
}

func (client *ECommerceAPIClient) UpdateOrder(orderID string, updateData map[string]interface{}) ([]byte, error) {
	endpoint := fmt.Sprintf("/orders/%s", orderID)
	return client.makeRequest("PUT", endpoint, updateData)
}

func (client *ECommerceAPIClient) DeleteOrder(orderID string) ([]byte, error) {
	endpoint := fmt.Sprintf("/orders/%s", orderID)
	return client.makeRequest("DELETE", endpoint, nil)
}
```

### models/product.go
```go
package models

type Product struct {
	ID          string  `json:"id"`
	Name        string  `json:"name"`
	Description string  `json:"description"`
	Price       float64 `json:"price"`
}
```

### models/order.go
```go
package models

type Order struct {
	ID              string       `json:"id"`
	CustomerID      string       `json:"customer_id"`
	Items           []OrderItem  `json:"items"`
	ShippingAddress string       `json:"shipping_address"`
	Status          string       `json:"status"`
}

type OrderItem struct {
	ProductID string `json:"product_id"`
	Quantity  int    `json:"quantity"`
}
```

### utils/helpers.go
```go
package utils

import (
	"encoding/json"
	"fmt"
)

func PrettyPrintJSON(data []byte) string {
	var out map[string]interface{}
	if err := json.Unmarshal(data, &out); err != nil {
		return fmt.Sprintf("Error parsing JSON: %v", err)
	}
	prettyJSON, err := json.MarshalIndent(out, "", "  ")
	if err != nil {
		return fmt.Sprintf("Error formatting JSON: %v", err)
	}
	return string(prettyJSON)
}

func HandleError(err error) {
	if err != nil {
		fmt.Printf("Error: %v\n", err)
	}
}
```

### tests/api_test.go
```go
package tests

import (
	"testing"
	"github.com/your_username/ecommerce-client/api"
)

func TestGetProducts(t *testing.T) {
	client := api.NewECommerceAPIClient("https://api.example.com", "test_api_key")
	_, err := client.GetProducts(nil)
	if err != nil {
		t.Errorf("Expected no error, got %v", err)
	}
}

func TestCreateOrder(t *testing.T) {
	client := api.NewECommerceAPIClient("https://api.example.com", "test_api_key")
	orderData := map[string]interface{}{
		"customer_id": "123",
		"items": []map[string]interface{}{
			{"product_id": "456", "quantity": 2},
		},
	}
	_, err := client.CreateOrder(orderData)
	if err != nil {
		t.Errorf("Expected no error, got %v", err)
	}
}

func TestGetOrderDetails(t *testing.T) {
	client := api.NewECommerceAPIClient("https://api.example.com", "test_api_key")
	_, err := client.GetOrderDetails("123")
	if err != nil {
		t.Errorf("Expected no error, got %v", err)
	}
}
```

### README.md
```markdown
# E-Commerce API Client

## Overview
This project demonstrates the implementation of an API client for an e-commerce system using Go. It supports operations like fetching products, creating and managing orders, and more.

## Setup
1. Clone the repository.
2. Replace `your_api_key_here` in `main.go` with your actual API key.
3. Run the application using:
   %mdticks%bash
   go run main.go
   %mdticks%
```

## Features
- Fetch product listings
- Get product details
- Create orders
- View, update, and delete orders

## Testing
Run the tests using:
```bash
go test ./...
```


