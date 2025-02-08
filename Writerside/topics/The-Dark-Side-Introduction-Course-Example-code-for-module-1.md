# Example code for module 1

Below are several Python code examples that illustrate key phases of a penetration testing engagement. These examples are intended for educational purposes only and should be executed **only in controlled and authorized environments**.

---

## Example 1: Reconnaissance – Domain Information Gathering

In the planning and reconnaissance phase, testers collect publicly available information about a target. For example, you can use a Python library to perform a WHOIS lookup:

```python
# recon_whois.py
import whois

def get_domain_info(domain):
    try:
        domain_info = whois.whois(domain)
        return domain_info
    except Exception as e:
        return f"Error retrieving WHOIS info: {e}"

if __name__ == '__main__':
    target_domain = "example.com"
    info = get_domain_info(target_domain)
    print(info)
```

*Before running this script, install the required package with:*
```bash
pip install python-whois
```

---

## Example 2: Scanning and Enumeration – Simple Port Scanner

A common step during the scanning phase is to enumerate open ports. The following script uses Python’s `socket` module to scan a range of ports on a target host:

```python
# port_scanner.py
import socket

def scan_ports(target, start_port, end_port):
    open_ports = []
    for port in range(start_port, end_port + 1):
        sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        sock.settimeout(0.5)
        result = sock.connect_ex((target, port))
        if result == 0:
            open_ports.append(port)
        sock.close()
    return open_ports

if __name__ == '__main__':
    target_ip = "127.0.0.1"  # Change this to your target's IP address
    start = 1
    end = 1024
    open_ports = scan_ports(target_ip, start, end)
    print(f"Open ports on {target_ip}: {open_ports}")
```

*Tip: Use this script only on networks you have permission to test.*

---

## Example 3: Exploitation – Demonstrating an SQL Injection Vulnerability

Below is a simple Flask application that simulates a vulnerable login endpoint. The example shows how improper handling of user inputs can lead to an SQL injection vulnerability.

> **Warning:** This code is deliberately vulnerable and should **never** be deployed in a production environment.

```python
# vulnerable_app.py
from flask import Flask, request
import sqlite3

app = Flask(__name__)

def init_db():
    conn = sqlite3.connect('test.db')
    c = conn.cursor()
    c.execute('''CREATE TABLE IF NOT EXISTS users (
                 id INTEGER PRIMARY KEY,
                 username TEXT,
                 password TEXT)''')
    # Insert sample data if not already present
    c.execute('''INSERT INTO users (username, password)
                 SELECT 'admin', 'admin123'
                 WHERE NOT EXISTS (
                     SELECT 1 FROM users WHERE username = 'admin'
                 )''')
    conn.commit()
    conn.close()

init_db()

@app.route('/login', methods=['GET'])
def login():
    username = request.args.get('username')
    password = request.args.get('password')
    # Vulnerable query (do not use in production)
    query = f"SELECT * FROM users WHERE username = '{username}' AND password = '{password}'"
    conn = sqlite3.connect('test.db')
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

*You can test the vulnerability by running the app and visiting a URL such as:*

```
http://127.0.0.1:5000/login?username=admin&password=admin123' OR '1'='1
```

This input may bypass authentication due to the SQL injection flaw.

---

## Example 4: Mitigation – Securing Against SQL Injection

To remediate the vulnerability demonstrated above, you should use parameterized queries. Here’s the corrected version of the Flask login endpoint:

```python
# secure_app.py
from flask import Flask, request
import sqlite3

app = Flask(__name__)

def init_db():
    conn = sqlite3.connect('test.db')
    c = conn.cursor()
    c.execute('''CREATE TABLE IF NOT EXISTS users (
                 id INTEGER PRIMARY KEY,
                 username TEXT,
                 password TEXT)''')
    c.execute('''INSERT INTO users (username, password)
                 SELECT 'admin', 'admin123'
                 WHERE NOT EXISTS (
                     SELECT 1 FROM users WHERE username = 'admin'
                 )''')
    conn.commit()
    conn.close()

init_db()

@app.route('/login', methods=['GET'])
def login():
    username = request.args.get('username')
    password = request.args.get('password')
    # Secure query using parameterized inputs
    query = "SELECT * FROM users WHERE username = ? AND password = ?"
    conn = sqlite3.connect('test.db')
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

*This version of the code uses placeholders (`?`) to ensure that user inputs are properly escaped, protecting against SQL injection attacks.*

---

## Example 5: Reporting – Generating a Vulnerability Report in JSON

After testing, a penetration tester typically compiles a detailed report. The following snippet shows how you might generate a simple JSON report summarizing findings:

```python
# generate_report.py
import json

def generate_report():
    report = {
        "vulnerabilities": [
            {
                "id": 1,
                "description": "SQL Injection vulnerability in /login endpoint",
                "severity": "High",
                "remediation": "Use parameterized queries to handle user input."
            },
            {
                "id": 2,
                "description": "Open port detected on port 80",
                "severity": "Medium",
                "remediation": "Implement proper firewall rules to restrict unnecessary services."
            }
        ],
        "summary": "2 vulnerabilities found. Immediate attention recommended for high severity issues."
    }
    with open('vulnerability_report.json', 'w') as f:
        json.dump(report, f, indent=4)
    print("Vulnerability report saved as vulnerability_report.json")

if __name__ == '__main__':
    generate_report()
```

*This report can be further expanded or formatted to meet organizational standards for security documentation.*

---

## Final Notes

These code examples demonstrate foundational techniques discussed in **Module 1: Penetration Testing 101**:
- **Reconnaissance:** Gathering public data (WHOIS lookup).
- **Scanning and Enumeration:** Identifying open ports.
- **Exploitation:** Demonstrating how vulnerabilities like SQL injection can be exploited.
- **Mitigation:** Correcting vulnerabilities with secure coding practices.
- **Reporting:** Documenting findings in an actionable format.

Remember, ethical hacking must always be performed with proper authorization and in compliance with legal requirements. Happy learning, and welcome to the exciting world of ethical hacking!