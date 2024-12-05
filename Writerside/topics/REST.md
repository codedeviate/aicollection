# REST

REST (Representational State Transfer) is an architectural style for designing networked applications. It relies on a stateless, client-server, cacheable communications protocol -- the HTTP protocol is almost always used. RESTful applications use HTTP requests to perform CRUD (Create, Read, Update, Delete) operations on resources, which are identified by URLs.

## Key Principles of REST:
1. **Stateless**: Each request from a client to server must contain all the information needed to understand and process the request. The server does not store any state about the client session.
2. **Client-Server**: The client and server are separate entities. The client makes requests, and the server processes them and returns the appropriate responses.
3. **Cacheable**: Responses must define themselves as cacheable or not to prevent clients from reusing stale or inappropriate data.
4. **Uniform Interface**: A consistent way of interacting with resources, typically using standard HTTP methods (GET, POST, PUT, DELETE).
5. **Layered System**: The client cannot ordinarily tell whether it is connected directly to the end server or to an intermediary along the way.
6. **Code on Demand (optional)**: Servers can temporarily extend or customize the functionality of a client by transferring executable code.

## Example in Python (using Flask):
```python
from flask import Flask, jsonify, request

app = Flask(__name__)

# In-memory database
books = [
    {'id': 1, 'title': '1984', 'author': 'George Orwell'},
    {'id': 2, 'title': 'To Kill a Mockingbird', 'author': 'Harper Lee'}
]

@app.route('/books', methods=['GET'])
def get_books():
    return jsonify(books)

@app.route('/books/<int:book_id>', methods=['GET'])
def get_book(book_id):
    book = next((book for book in books if book['id'] == book_id), None)
    return jsonify(book) if book else ('', 404)

@app.route('/books', methods=['POST'])
def add_book():
    new_book = request.get_json()
    books.append(new_book)
    return jsonify(new_book), 201

@app.route('/books/<int:book_id>', methods=['PUT'])
def update_book(book_id):
    book = next((book for book in books if book['id'] == book_id), None)
    if book:
        data = request.get_json()
        book.update(data)
        return jsonify(book)
    return ('', 404)

@app.route('/books/<int:book_id>', methods=['DELETE'])
def delete_book(book_id):
    global books
    books = [book for book in books if book['id'] != book_id]
    return ('', 204)

if __name__ == '__main__':
    app.run(debug=True)
```

## Example in JavaScript (using Express.js):
```javascript
const express = require('express');
const app = express();
app.use(express.json());

let books = [
    { id: 1, title: '1984', author: 'George Orwell' },
    { id: 2, title: 'To Kill a Mockingbird', author: 'Harper Lee' }
];

app.get('/books', (req, res) => {
    res.json(books);
});

app.get('/books/:id', (req, res) => {
    const book = books.find(b => b.id === parseInt(req.params.id));
    if (!book) return res.status(404).send('Book not found');
    res.json(book);
});

app.post('/books', (req, res) => {
    const newBook = req.body;
    books.push(newBook);
    res.status(201).json(newBook);
});

app.put('/books/:id', (req, res) => {
    const book = books.find(b => b.id === parseInt(req.params.id));
    if (!book) return res.status(404).send('Book not found');
    Object.assign(book, req.body);
    res.json(book);
});

app.delete('/books/:id', (req, res) => {
    books = books.filter(b => b.id !== parseInt(req.params.id));
    res.status(204).send();
});

app.listen(3000, () => {
    console.log('Server is running on port 3000');
});
```

## Example in Java (using Spring Boot):
```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.*;

import java.util.ArrayList;
import java.util.List;
import java.util.Optional;

@SpringBootApplication
public class RestApplication {
    public static void main(String[] args) {
        SpringApplication.run(RestApplication.class, args);
    }
}

@RestController
@RequestMapping("/books")
class BookController {
    private List<Book> books = new ArrayList<>();

    public BookController() {
        books.add(new Book(1, "1984", "George Orwell"));
        books.add(new Book(2, "To Kill a Mockingbird", "Harper Lee"));
    }

    @GetMapping
    public List<Book> getBooks() {
        return books;
    }

    @GetMapping("/{id}")
    public Book getBook(@PathVariable int id) {
        return books.stream().filter(book -> book.getId() == id).findFirst().orElse(null);
    }

    @PostMapping
    public Book addBook(@RequestBody Book newBook) {
        books.add(newBook);
        return newBook;
    }

    @PutMapping("/{id}")
    public Book updateBook(@PathVariable int id, @RequestBody Book updatedBook) {
        Optional<Book> bookOptional = books.stream().filter(book -> book.getId() == id).findFirst();
        if (bookOptional.isPresent()) {
            Book book = bookOptional.get();
            book.setTitle(updatedBook.getTitle());
            book.setAuthor(updatedBook.getAuthor());
            return book;
        }
        return null;
    }

    @DeleteMapping("/{id}")
    public void deleteBook(@PathVariable int id) {
        books.removeIf(book -> book.getId() == id);
    }
}

class Book {
    private int id;
    private String title;
    private String author;

    public Book(int id, String title, String author) {
        this.id = id;
        this.title = title;
        this.author = author;
    }

    // Getters and setters omitted for brevity
}
```
