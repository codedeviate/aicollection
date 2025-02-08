# Example code for module 2

Below are several code examples that illustrate common attack vectors discussed in **Module 2: Dissecting Attack Vectors – How Cybercriminals Exploit Vulnerabilities**. Each example demonstrates a vulnerability and—in many cases—a corresponding mitigation strategy. **Always run these examples only in controlled, authorized, and safe environments.**

---

## 1. SQL Injection

### Vulnerable Example SQL Injection

This Flask application simulates a login endpoint that uses string concatenation to build a SQL query, making it vulnerable to SQL injection attacks.

```python
# vulnerable_sql_app.py
from flask import Flask, request
import sqlite3

app = Flask(__name__)

def init_db():
    conn = sqlite3.connect('database.db')
    c = conn.cursor()
    c.execute('''CREATE TABLE IF NOT EXISTS users (
                    id INTEGER PRIMARY KEY,
                    username TEXT,
                    password TEXT)''')
    # Insert a sample user
    c.execute("INSERT INTO users (username, password) VALUES ('admin', 'password123')")
    conn.commit()
    conn.close()

init_db()

@app.route('/login', methods=['GET'])
def login():
    username = request.args.get('username')
    password = request.args.get('password')
    # Vulnerable query: using string concatenation allows attackers to inject SQL code.
    query = "SELECT * FROM users WHERE username = '" + username + "' AND password = '" + password + "'"
    conn = sqlite3.connect('database.db')
    c = conn.cursor()
    c.execute(query)
    user = c.fetchone()
    conn.close()
    if user:
        return "Login successful!"
    else:
        return "Login failed!"

if __name__ == '__main__':
    app.run(debug=True)
```

### Mitigated Example SQL Injection

Using parameterized queries prevents attackers from altering the SQL command structure.

```python
# secure_sql_app.py
from flask import Flask, request
import sqlite3

app = Flask(__name__)

def init_db():
    conn = sqlite3.connect('database.db')
    c = conn.cursor()
    c.execute('''CREATE TABLE IF NOT EXISTS users (
                    id INTEGER PRIMARY KEY,
                    username TEXT,
                    password TEXT)''')
    # Insert a sample user
    c.execute("INSERT INTO users (username, password) VALUES ('admin', 'password123')")
    conn.commit()
    conn.close()

init_db()

@app.route('/login', methods=['GET'])
def login():
    username = request.args.get('username')
    password = request.args.get('password')
    # Secure query using parameterized inputs
    query = "SELECT * FROM users WHERE username = ? AND password = ?"
    conn = sqlite3.connect('database.db')
    c = conn.cursor()
    c.execute(query, (username, password))
    user = c.fetchone()
    conn.close()
    if user:
        return "Login successful!"
    else:
        return "Login failed!"

if __name__ == '__main__':
    app.run(debug=True)
```

---

## 2. Cross-Site Scripting (XSS)

### Vulnerable Example XSS

This Flask endpoint directly embeds user-supplied data into the HTML response without escaping, opening the door for XSS attacks.

```python
# vulnerable_xss_app.py
from flask import Flask, request, render_template_string

app = Flask(__name__)

@app.route('/comment', methods=['GET'])
def comment():
    user_comment = request.args.get('comment', '')
    # Vulnerable: Directly embedding unsanitized user input
    html = f"<h1>User Comment</h1><p>{user_comment}</p>"
    return render_template_string(html)

if __name__ == '__main__':
    app.run(debug=True)
```

*Example Attack:*  
A URL such as:
```
http://127.0.0.1:5000/comment?comment=<script>alert('XSS');</script>
```  
will cause the browser to execute the injected script.

### Mitigated Example XSS

Using a template with autoescaping (the default in Jinja2) prevents malicious scripts from executing.

```python
# secure_xss_app.py
from flask import Flask, request, render_template_string

app = Flask(__name__)

@app.route('/comment', methods=['GET'])
def comment():
    user_comment = request.args.get('comment', '')
    # Secure: Use a template with autoescaping enabled.
    template = """
    <h1>User Comment</h1>
    <p>{{ comment }}</p>
    """
    return render_template_string(template, comment=user_comment)

if __name__ == '__main__':
    app.run(debug=True)
```

---

## 3. Command Injection

### Vulnerable Example Command Injection

This Flask endpoint accepts a target host to ping and constructs a system command by concatenating unsanitized input, leading to potential command injection.

```python
# vulnerable_command_injection.py
import os
from flask import Flask, request

app = Flask(__name__)

@app.route('/ping', methods=['GET'])
def ping():
    target = request.args.get('target', '')
    # Vulnerable: Unsanitized input used directly in a system command.
    command = "ping -c 4 " + target
    stream = os.popen(command)
    output = stream.read()
    return "<pre>" + output + "</pre>"

if __name__ == '__main__':
    app.run(debug=True)
```

### Mitigated Example Command Injection

Validating input and using safe command execution methods (such as passing arguments as a list with `subprocess.run`) mitigates this risk.

```python
# secure_command_injection.py
import subprocess
from flask import Flask, request, abort
import re

app = Flask(__name__)

def is_valid_hostname(hostname):
    # Basic validation: allow letters, numbers, dots, and hyphens.
    pattern = re.compile(r'^([a-zA-Z0-9.-]+)$')
    return pattern.match(hostname)

@app.route('/ping', methods=['GET'])
def ping():
    target = request.args.get('target', '')
    if not target or not is_valid_hostname(target):
        abort(400, "Invalid target")
    # Secure: Use subprocess.run with a list of arguments.
    try:
        result = subprocess.run(["ping", "-c", "4", target],
                                capture_output=True, text=True, check=True)
        output = result.stdout
    except subprocess.CalledProcessError as e:
        output = e.output
    return "<pre>" + output + "</pre>"

if __name__ == '__main__':
    app.run(debug=True)
```

---

## 4. Buffer Overflow (C Example)

### Vulnerable Example Buffer Overflow

The following C code uses the unsafe `gets()` function, which does not check the length of the input and can lead to a buffer overflow.

```c
// vulnerable_buffer_overflow.c
#include <stdio.h>
#include <string.h>

void vulnerable_function() {
    char buffer[64];
    printf("Enter some text: ");
    // Vulnerable: gets() does not enforce bounds checking.
    gets(buffer);
    printf("You entered: %s\n", buffer);
}

int main() {
    vulnerable_function();
    return 0;
}
```

### Mitigated Example Buffer Overflow

Replacing `gets()` with `fgets()` allows you to specify the maximum number of characters to read, preventing overflow.

```c
// secure_buffer_overflow.c
#include <stdio.h>
#include <string.h>

void secure_function() {
    char buffer[64];
    printf("Enter some text: ");
    // Secure: fgets() limits the number of characters read.
    if (fgets(buffer, sizeof(buffer), stdin) != NULL) {
        // Optionally remove the newline character.
        size_t len = strlen(buffer);
        if (len > 0 && buffer[len - 1] == '\n') {
            buffer[len - 1] = '\0';
        }
        printf("You entered: %s\n", buffer);
    }
}

int main() {
    secure_function();
    return 0;
}
```

---

## 5. File Inclusion Vulnerability (PHP Example)

### Vulnerable Example File Inclusion

This PHP snippet demonstrates a file inclusion vulnerability by directly including a file specified via user input without validation.

```php
<?php
// vulnerable_file_inclusion.php

if (isset($_GET['page'])) {
    $page = $_GET['page'];
    // Vulnerable: Directly including a file based on user input.
    include($page);
} else {
    echo "No page specified.";
}
?>
```

### Mitigated Example File Inclusion

Using a whitelist of allowed pages ensures that only known, safe files can be included.

```php
<?php
// secure_file_inclusion.php

// Define a whitelist of allowed files.
$allowed_pages = ['home.php', 'about.php', 'contact.php'];

if (isset($_GET['page'])) {
    $page = $_GET['page'];
    if (in_array($page, $allowed_pages)) {
        include($page);
    } else {
        echo "Invalid page requested.";
    }
} else {
    echo "No page specified.";
}
?>
```

---

## Final Notes

These examples cover several common attack vectors:
- **SQL Injection:** Demonstrates how improper query construction can lead to unauthorized database access.
- **Cross-Site Scripting (XSS):** Shows how unsanitized user input in HTML can result in malicious script execution.
- **Command Injection:** Illustrates the risks of executing system commands with unsanitized input.
- **Buffer Overflow:** Provides a C example of unsafe memory handling.
- **File Inclusion:** Explains how unsanitized file paths can allow unauthorized file access.

By understanding both the vulnerabilities and the appropriate mitigations, you can better design systems to resist real-world attacks. Remember, ethical hacking and penetration testing must always be performed with explicit authorization and within legal boundaries.

Happy learning, and stay vigilant!