# Example code for module 9

Below are several code examples that illustrate legal and ethical best practices described in **Module 9: Legal and Ethical Considerations in Penetration Testing**. These examples focus on two key areas:

1. **Authorization Verification:**  
   Before beginning any testing, it is critical to ensure that you have explicit, documented permission. The sample below reads a JSON-formatted authorization file that contains details such as consent status and the defined scope of the engagement.

2. **Secure Data Handling and Logging:**  
   Penetration tests often collect sensitive information. To comply with data protection laws and ethical guidelines, you should handle and store such data securely. The secure logging example below uses symmetric encryption (via the Python _cryptography_ library) to encrypt log entries, ensuring that sensitive information is protected.

> **Disclaimer:**  
> Use these examples only on systems and networks for which you have explicit authorization. These samples are for educational purposes in controlled lab environments only.

---

## Example 1: Authorization Verification

This Python script checks for an "authorization.json" file that must be provided by the system owner. The file should include a flag (e.g., `"authorized": true`) and may include other details such as the test scope. The script halts execution if the authorization is missing or invalid.

```python
# authorization_check.py
import json
import sys

def check_authorization(file_path):
    try:
        with open(file_path, 'r') as f:
            auth_data = json.load(f)
    except FileNotFoundError:
        print("Authorization file not found. Aborting test.")
        sys.exit(1)
    except json.JSONDecodeError:
        print("Invalid JSON format in authorization file. Aborting test.")
        sys.exit(1)

    if not auth_data.get("authorized", False):
        print("Test not authorized. Aborting.")
        sys.exit(1)

    print("Authorization verified. Test may proceed.")
    # Optionally, print the defined scope
    scope = auth_data.get("scope", "No scope defined")
    print(f"Scope: {scope}")

if __name__ == '__main__':
    # Ensure the 'authorization.json' file exists and contains the required authorization details.
    check_authorization("authorization.json")
```

*Sample `authorization.json` file:*

```json
{
    "authorized": true,
    "scope": "Test systems: 192.168.1.100-192.168.1.110, Web applications: example.com/login"
}
```

---

## Example 2: Secure Logging with Encryption

This script demonstrates how to encrypt sensitive log data before writing it to a file. It uses the _cryptography_ library's Fernet symmetric encryption to ensure that log entries (which might contain details of vulnerabilities or other sensitive information) are stored securely.

> **Prerequisites:**  
> Install the required package with:
> ```bash
> pip install cryptography
> ```

```python
# secure_logging.py
from cryptography.fernet import Fernet
import json
import datetime

# Generate and save a key (do this once and store the key securely)
def generate_key():
    key = Fernet.generate_key()
    with open("secret.key", "wb") as key_file:
        key_file.write(key)
    return key

# Load the encryption key from a file
def load_key():
    try:
        with open("secret.key", "rb") as key_file:
            return key_file.read()
    except FileNotFoundError:
        return generate_key()

def encrypt_log(message, key):
    fernet = Fernet(key)
    encrypted_message = fernet.encrypt(message.encode())
    return encrypted_message

def log_event_securely(event_description, log_file="secure_log.enc"):
    key = load_key()
    timestamp = datetime.datetime.now().isoformat()
    log_entry = {"timestamp": timestamp, "event": event_description}
    log_entry_json = json.dumps(log_entry)
    encrypted_entry = encrypt_log(log_entry_json, key)
    with open(log_file, "ab") as f:
        f.write(encrypted_entry + b"\n")
    print(f"Logged event securely: {log_entry_json}")

if __name__ == '__main__':
    # Example: Log a test event that indicates the start of an authorized penetration test.
    log_event_securely("Test event: Penetration test initiated under authorized scope.")
```

*What This Does:*
- **Key Management:**  
  The script attempts to load an existing encryption key from `secret.key` (or generates one if it does not exist). In a production scenario, manage and store this key securely.

- **Encryption and Logging:**  
  Each log entry (with a timestamp and event description) is encrypted before being appended to the log file (`secure_log.enc`). This ensures that even if the log file is accessed by unauthorized parties, its contents remain protected.

---

## Final Notes

These code examples embody key legal and ethical practices in penetration testing:

- **Authorization Verification:**  
  Always confirm that you have written permission before conducting any tests. Use tools or scripts to validate that proper documentation exists.

- **Secure Data Handling:**  
  Encrypt sensitive information—such as penetration test logs, vulnerability data, or any findings—to ensure compliance with data protection laws and ethical guidelines.

By incorporating these practices into your testing framework, you not only protect the integrity and confidentiality of your test data but also demonstrate a commitment to ethical conduct and legal compliance. These measures help build trust with clients and safeguard both your practice and the systems you test.

*As you continue your journey in ethical hacking, remember: legal compliance and ethical responsibility are as crucial as technical expertise.*