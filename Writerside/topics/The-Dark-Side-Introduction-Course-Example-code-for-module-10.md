# Example code for module 10

Below are several example code snippets that illustrate proactive measures and emerging trends described in **Module 10: The Future of Cyber Threats – Preparing for the Next Wave of Attacks**. These examples are meant for educational purposes and should be run only in controlled, authorized lab environments.

---

## Example 1: IoT Vulnerability Scanner Simulation

One major emerging threat is the proliferation of insecure IoT devices. This script simulates scanning a list of IoT devices (represented by dummy IP addresses) to check whether they are using default credentials—a common vulnerability in IoT deployments.

```python
# iot_vulnerability_scanner.py
import random

# Simulated list of IoT devices with their IP addresses and credentials status.
iot_devices = [
    {"ip": "192.168.1.101", "device": "Smart Camera", "default_creds": True},
    {"ip": "192.168.1.102", "device": "Smart Thermostat", "default_creds": False},
    {"ip": "192.168.1.103", "device": "Smart Lock", "default_creds": True},
    {"ip": "192.168.1.104", "device": "Smart Light", "default_creds": False},
    {"ip": "192.168.1.105", "device": "Smart Speaker", "default_creds": random.choice([True, False])},
]

def scan_devices(devices):
    vulnerable = []
    print("Starting IoT vulnerability scan...\n")
    for device in devices:
        # In a real scanner, you might try to log in with default credentials.
        if device["default_creds"]:
            vulnerable.append(device)
            print(f"[VULNERABLE] {device['device']} at {device['ip']} uses default credentials!")
        else:
            print(f"[OK] {device['device']} at {device['ip']} appears secure.")
    return vulnerable

if __name__ == '__main__':
    vulnerable_devices = scan_devices(iot_devices)
    print("\nScan complete.")
    if vulnerable_devices:
        print(f"Vulnerable devices found: {len(vulnerable_devices)}")
    else:
        print("No vulnerable devices detected.")
```

*What It Does:*
- Simulates scanning a set of IoT devices.
- Flags devices that are using default credentials.
- Demonstrates the importance of securing IoT endpoints as part of a risk-based security approach.

---

## Example 2: Threat Intelligence Feed Integration and Risk Scoring

Staying ahead of emerging threats requires continuous monitoring of threat intelligence. This script simulates reading a threat intelligence feed from a local JSON file, calculates a risk score for a set of assets, and outputs alerts based on the current threat level.

> **Note:** In a real-world scenario, the feed might come from an external API or SIEM system.

```python
# threat_intel_risk_scoring.py
import json
import datetime

# Simulated threat intelligence feed (normally retrieved via an API)
threat_intel_feed = {
    "timestamp": datetime.datetime.now().isoformat(),
    "threats": [
        {"category": "IoT", "severity": 8, "description": "Default credentials exploited on smart devices."},
        {"category": "Cloud", "severity": 6, "description": "Misconfiguration of S3 buckets detected."},
        {"category": "Mobile", "severity": 4, "description": "Vulnerable mobile app version in circulation."},
        {"category": "AI", "severity": 7, "description": "Adversarial AI techniques bypassing standard filters."}
    ]
}

# Simulated asset risk profile for an organization
assets = [
    {"name": "IoT Camera System", "category": "IoT", "base_risk": 5},
    {"name": "Cloud Storage Service", "category": "Cloud", "base_risk": 4},
    {"name": "Corporate Mobile App", "category": "Mobile", "base_risk": 3},
    {"name": "User Authentication Service", "category": "AI", "base_risk": 6}
]

def calculate_risk(asset, threats):
    # Increase asset risk score if there is a matching threat from the feed.
    risk = asset["base_risk"]
    for threat in threats:
        if asset["category"] == threat["category"]:
            risk += threat["severity"] * 0.1  # Weight factor for threat impact
    return round(risk, 2)

def risk_assessment(assets, threat_feed):
    print(f"Threat Intelligence Timestamp: {threat_feed['timestamp']}\n")
    for asset in assets:
        risk_score = calculate_risk(asset, threat_feed["threats"])
        print(f"Asset: {asset['name']} (Category: {asset['category']}) -> Risk Score: {risk_score}")
        if risk_score > 7:
            print("  ALERT: High risk detected! Immediate action recommended.\n")
        else:
            print("  Risk level is acceptable under current threat conditions.\n")

if __name__ == '__main__':
    risk_assessment(assets, threat_intel_feed)
```

*What It Does:*
- Reads a simulated threat intelligence feed.
- Computes a dynamic risk score for each asset by combining a base risk value with threat severity.
- Outputs alerts for assets that exceed a risk threshold.
- Illustrates the integration of threat intelligence into a proactive, risk-based defense strategy.

---

## Example 3: Quantum-Resistant Encryption (Placeholder)

Quantum computing poses a future threat to classical encryption methods. Although full-fledged post-quantum cryptographic algorithms are still emerging, organizations are beginning to plan for the transition. This example provides a placeholder for a quantum-resistant encryption function. For now, it uses AES encryption (from the _pycryptodome_ library) while noting that in a production environment, you should transition to a quantum-safe algorithm when available.

> **Prerequisites:**  
> Install PyCryptodome with:
> ```bash
> pip install pycryptodome
> ```

```python
# quantum_resistant_encryption.py
from Crypto.Cipher import AES
from Crypto.Random import get_random_bytes
import base64

def classical_encrypt(data, key):
    cipher = AES.new(key, AES.MODE_EAX)
    nonce = cipher.nonce
    ciphertext, tag = cipher.encrypt_and_digest(data.encode())
    return base64.b64encode(nonce + tag + ciphertext).decode()

def quantum_resistant_encrypt(data, key):
    """
    Placeholder for quantum-resistant encryption.
    In a future implementation, replace this with a quantum-safe algorithm
    (e.g., lattice-based cryptography). For now, we use classical AES encryption.
    """
    print("Warning: Using classical AES encryption. Upgrade to quantum-resistant algorithm when available.")
    return classical_encrypt(data, key)

if __name__ == '__main__':
    key = get_random_bytes(16)  # AES-128 bit key; in practice, secure key management is essential.
    sensitive_data = "Confidential data that requires protection against future quantum threats."
    
    encrypted_data = quantum_resistant_encrypt(sensitive_data, key)
    print("Encrypted data:")
    print(encrypted_data)
```

*What It Does:*
- Provides a function for classical AES encryption.
- Wraps the AES function in a placeholder for a quantum-resistant encryption routine.
- Reminds the user to plan for upgrading to quantum-safe cryptographic algorithms in the future.
- Demonstrates forward-thinking by simulating how legacy methods might be replaced in a future-proof security strategy.

---

## Final Notes

These examples illustrate how to prepare for future cyber threats by:

- **Securing Emerging Technologies:**  
  Simulating an IoT vulnerability scan underscores the importance of protecting increasingly connected devices.

- **Integrating Threat Intelligence:**  
  The risk scoring script shows how continuous monitoring of threat feeds can drive proactive, risk-based decision-making.

- **Planning for Quantum Challenges:**  
  The encryption placeholder highlights the need to begin planning for quantum-resistant cryptography as part of long-term security strategies.

By incorporating these techniques into your security program, you can better anticipate and mitigate the next wave of cyber attacks. Stay informed, proactive, and adaptive in the ever-changing landscape of cybersecurity.

*Happy coding, and may your defenses be as innovative as the threats you prepare for!*