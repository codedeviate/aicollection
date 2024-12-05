# CRUD

CRUD stands for Create, Read, Update, and Delete. These are the four basic operations that can be performed on data in a database or a similar storage system. Here's a detailed explanation of each operation:

1. **Create**: Adds new data to the database.
2. **Read**: Retrieves data from the database.
3. **Update**: Modifies existing data in the database.
4. **Delete**: Removes data from the database.

## Example in Python (using Flask):
```python
from flask import Flask, jsonify, request

app = Flask(__name__)

# In-memory database
items = []

@app.route('/items', methods=['POST'])
def create_item():
    new_item = request.get_json()
    items.append(new_item)
    return jsonify(new_item), 201

@app.route('/items', methods=['GET'])
def read_items():
    return jsonify(items)

@app.route('/items/<int:item_id>', methods=['GET'])
def read_item(item_id):
    item = next((item for item in items if item['id'] == item_id), None)
    return jsonify(item) if item else ('', 404)

@app.route('/items/<int:item_id>', methods=['PUT'])
def update_item(item_id):
    item = next((item for item in items if item['id'] == item_id), None)
    if item:
        data = request.get_json()
        item.update(data)
        return jsonify(item)
    return ('', 404)

@app.route('/items/<int:item_id>', methods=['DELETE'])
def delete_item(item_id):
    global items
    items = [item for item in items if item['id'] != item_id]
    return ('', 204)

if __name__ == '__main__':
    app.run(debug=True)
```

## Example in JavaScript (using Express.js):
```javascript
const express = require('express');
const app = express();
app.use(express.json());

let items = [];

app.post('/items', (req, res) => {
    const newItem = req.body;
    items.push(newItem);
    res.status(201).json(newItem);
});

app.get('/items', (req, res) => {
    res.json(items);
});

app.get('/items/:id', (req, res) => {
    const item = items.find(i => i.id === parseInt(req.params.id));
    if (!item) return res.status(404).send('Item not found');
    res.json(item);
});

app.put('/items/:id', (req, res) => {
    const item = items.find(i => i.id === parseInt(req.params.id));
    if (!item) return res.status(404).send('Item not found');
    Object.assign(item, req.body);
    res.json(item);
});

app.delete('/items/:id', (req, res) => {
    items = items.filter(i => i.id !== parseInt(req.params.id));
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
public class CrudApplication {
    public static void main(String[] args) {
        SpringApplication.run(CrudApplication.class, args);
    }
}

@RestController
@RequestMapping("/items")
class ItemController {
    private List<Item> items = new ArrayList<>();

    @PostMapping
    public Item createItem(@RequestBody Item newItem) {
        items.add(newItem);
        return newItem;
    }

    @GetMapping
    public List<Item> readItems() {
        return items;
    }

    @GetMapping("/{id}")
    public Item readItem(@PathVariable int id) {
        return items.stream().filter(item -> item.getId() == id).findFirst().orElse(null);
    }

    @PutMapping("/{id}")
    public Item updateItem(@PathVariable int id, @RequestBody Item updatedItem) {
        Optional<Item> itemOptional = items.stream().filter(item -> item.getId() == id).findFirst();
        if (itemOptional.isPresent()) {
            Item item = itemOptional.get();
            item.setName(updatedItem.getName());
            item.setValue(updatedItem.getValue());
            return item;
        }
        return null;
    }

    @DeleteMapping("/{id}")
    public void deleteItem(@PathVariable int id) {
        items.removeIf(item -> item.getId() == id);
    }
}

class Item {
    private int id;
    private String name;
    private String value;

    public Item(int id, String name, String value) {
        this.id = id;
        this.name = name;
        this.value = value;
    }

    // Getters and setters omitted for brevity
}
```