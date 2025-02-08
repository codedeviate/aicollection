# Example code for module 8

Below are several code examples that illustrate real-world vulnerabilities described in **Module 8: Case Studies in Penetration Testing – Real-World Breaches and Lessons Learned**. These examples simulate common attack techniques that led to major breaches in the case studies, along with simple remediation approaches. **Use these examples only in controlled, authorized lab environments for educational purposes.**

---

## Example 1: SQL Injection Breach Simulation

This example demonstrates a vulnerable web login endpoint written in Python using Flask. In the simulated retail breach, the application does not properly sanitize user inputs, allowing an attacker to inject malicious SQL commands (e.g., using the payload `' OR '1'='1`). Later, a secure version would use parameterized queries to fix the vulnerability.

### Vulnerable SQL Injection Application

```python
# vulnerable_sql_app.py
from flask import Flask, request
import sqlite3

app = Flask(__name__)

def init_db():
    conn = sqlite3.connect('retail.db')
    cursor = conn.cursor()
    cursor.execute('''CREATE TABLE IF NOT EXISTS users (
                        id INTEGER PRIMARY KEY,
                        username TEXT,
                        password TEXT)''')
    # Insert a sample user (for demonstration purposes)
    cursor.execute("INSERT INTO users (username, password) VALUES ('customer', 'securepass')")
    conn.commit()
    conn.close()

init_db()

@app.route('/login', methods=['GET'])
def login():
    username = request.args.get('username')
    password = request.args.get('password')
    # Vulnerable query: directly concatenates user input into SQL query
    query = f"SELECT * FROM users WHERE username = '{username}' AND password = '{password}'"
    conn = sqlite3.connect('retail.db')
    cursor = conn.cursor()
    cursor.execute(query)
    user = cursor.fetchone()
    conn.close()
    if user:
        return "Login successful! (This simulates unauthorized access.)"
    else:
        return "Login failed!"

if __name__ == '__main__':
    app.run(debug=True)
```

*Key Points for Case Study 1:*
- **Attack Flow:**
    - **Reconnaissance:** The attacker searches for input fields.
    - **Injection:** Using a payload like `' OR '1'='1` bypasses authentication.
    - **Data Extraction:** The attacker gains unauthorized access to the database.
- **Lessons Learned:**
    - Always use parameterized queries and input validation to protect against SQL injection.

---

## Example 2: Cross-Site Scripting (XSS) Vulnerability Simulation

This example simulates a vulnerable comment section on a social media platform using Flask. Here, user input is rendered without proper sanitization, allowing an attacker to inject and execute malicious JavaScript.

### Vulnerable XSS Application

```python
# vulnerable_xss_app.py
from flask import Flask, request, render_template_string

app = Flask(__name__)

@app.route('/comment', methods=['GET', 'POST'])
def comment():
    message = ""
    if request.method == 'POST':
        comment_text = request.form.get('comment')
        # Vulnerable: directly including unsanitized user input in the HTML response.
        message = f"User comment: {comment_text}"
    return render_template_string('''
        <html>
            <head>
                <title>Social Media Comments</title>
            </head>
            <body>
                <h2>Leave a Comment</h2>
                <form method="post">
                    <textarea name="comment" rows="4" cols="50"></textarea><br>
                    <input type="submit" value="Post Comment">
                </form>
                <div>{{ message|safe }}</div>
            </body>
        </html>
    ''', message=message)

if __name__ == '__main__':
    app.run(debug=True)
```

*Key Points for Case Study 2:*
- **Attack Flow:**
    - **Vulnerability Identification:** An attacker notices that the comment field does not sanitize input.
    - **Script Injection:** Malicious JavaScript (e.g., `<script>alert('XSS');</script>`) is injected.
    - **Impact:** When other users view the comment, the script executes, potentially stealing session data.
- **Lessons Learned:**
    - Use proper output encoding and sanitization (or template autoescaping) to prevent XSS.
    - Enforce a strict Content Security Policy (CSP).

---

## Example 3: Buffer Overflow Vulnerability Simulation

This C example demonstrates a classic buffer overflow vulnerability. The legacy application uses the unsafe `gets()` function to read user input, which can be exploited by providing input that exceeds the buffer’s capacity.

### Vulnerable Buffer Overflow Application (C)

```c
// vulnerable_buffer_overflow.c
#include <stdio.h>
#include <stdlib.h>

void vulnerable_function() {
    char buffer[64];
    printf("Enter input: ");
    // Vulnerable: gets() does not limit the number of characters read
    gets(buffer);
    printf("You entered: %s\n", buffer);
}

int main() {
    vulnerable_function();
    return 0;
}
```

### Remediated Version Using Safe Input (C)

```c
// secure_buffer_overflow.c
#include <stdio.h>
#include <stdlib.h>

void secure_function() {
    char buffer[64];
    printf("Enter input: ");
    // Secure: fgets() limits input to the size of the buffer
    if (fgets(buffer, sizeof(buffer), stdin) != NULL) {
        // Optionally remove newline character if present
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

*Key Points for Case Study 3:*
- **Attack Flow:**
    - **Discovery:** Penetration testers find that the application does not perform bounds checking.
    - **Exploit Execution:** An attacker inputs data longer than 64 characters, overflowing the buffer and enabling arbitrary code execution.
    - **Impact:** The attack demonstrates potential for complete system compromise.
- **Lessons Learned:**
    - Always use safe input functions (like `fgets()`).
    - Regularly update and patch legacy systems to modern standards.

---

## Example 4: Timeline Logger for Breach Analysis

This Python script simulates logging key events in an attack timeline. Such logging can help forensic teams reconstruct the sequence of events during a breach, similar to how investigators analyzed the case studies.

```python
# breach_timeline_logger.py
import logging
import datetime

# Configure logging to include timestamps
logging.basicConfig(level=logging.INFO, format='%(asctime)s - %(message)s', datefmt='%pct%Y-%pct%m-%pct%d %pct%H:%pct%M:%pct%S')

def log_event(event_description):
    logging.info(event_description)

if __name__ == '__main__':
    log_event("Reconnaissance: Probing public pages and search forms for vulnerabilities.")
    log_event("Injection: Payload \"' OR '1'='1\" used in login field to bypass authentication.")
    log_event("Data Extraction: Sensitive customer data retrieved from the database.")
    log_event("Detection: Unusual database query patterns detected by monitoring systems.")
```

*Key Points for Analysis:*
- **Purpose:**
    - Logs a timeline of events to help security teams understand the breach progression.
    - Provides a reference for what to monitor and how early detection could mitigate damage.
- **Application:**
    - In real incidents, detailed logs guide incident response and help refine security measures.

---

## Final Notes

These code examples illustrate real-world vulnerabilities and the lessons learned from past breaches:
- **SQL Injection:** Demonstrates the critical need for input validation and the use of parameterized queries.
- **Cross-Site Scripting (XSS):** Highlights the dangers of unsanitized user input and the importance of proper content handling.
- **Buffer Overflow:** Shows the risks inherent in legacy code and the importance of safe programming practices.
- **Timeline Logging:** Emphasizes the value of detailed logging and monitoring for incident analysis and improved defensive strategies.

By studying these case studies and experimenting with these examples in a controlled lab environment, security professionals can gain valuable insights into how breaches occur and how to better defend against them. Use these lessons to drive continuous improvement in your security posture.

*Happy learning, and remember: real-world breaches provide invaluable lessons—apply them to build stronger, more resilient defenses!*