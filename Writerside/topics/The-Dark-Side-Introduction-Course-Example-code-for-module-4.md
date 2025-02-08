# Example code for module 4

Below are several example scripts that illustrate how to simulate social engineering techniques in a controlled, ethical, and educational environment. **These examples are for training and awareness purposes only. They must never be used without explicit authorization and proper safeguards.**

---

## 1. Phishing Email Simulation

This Python script demonstrates how one might simulate sending a phishing email for training purposes. It uses Python’s built‑in libraries to construct and send an email via SMTP. **(Do not use this script to send unsolicited emails.)**

```python
# phishing_email_simulation.py
import smtplib
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText

# Configuration for SMTP (Example uses Gmail's SMTP server)
smtp_server = 'smtp.gmail.com'
smtp_port = 587
sender_email = 'your.email@gmail.com'
sender_password = 'yourpassword'  # In production, use environment variables or secure storage

# Target email for the simulation (must be a consenting recipient)
target_email = 'target@example.com'

def send_phishing_email():
    subject = "Urgent: Your Account Requires Immediate Verification"
    body = (
        "Dear User,\n\n"
        "We have detected unusual activity on your account. To secure your account, please verify "
        "your identity by clicking the link below:\n\n"
        "http://example.com/verify-your-account\n\n"
        "Failure to verify may result in temporary suspension of your account.\n\n"
        "Regards,\n"
        "IT Support Team"
    )

    msg = MIMEMultipart()
    msg['From'] = sender_email
    msg['To'] = target_email
    msg['Subject'] = subject
    msg.attach(MIMEText(body, 'plain'))

    try:
        server = smtplib.SMTP(smtp_server, smtp_port)
        server.starttls()  # Secure the connection
        server.login(sender_email, sender_password)
        server.sendmail(sender_email, target_email, msg.as_string())
        server.quit()
        print("Phishing email simulation sent successfully.")
    except Exception as e:
        print("Failed to send email:", e)

if __name__ == '__main__':
    send_phishing_email()
```

---

## 2. Simulated Phishing Webpage (Fake Login Page)

This Flask application simulates a fake login page commonly used in phishing attacks. It is designed for security training to help users recognize suspicious login pages. **Never deploy such pages in a live environment.**

```python
# fake_login.py
from flask import Flask, request

app = Flask(__name__)

@app.route('/', methods=['GET', 'POST'])
def login():
    message = ""
    if request.method == 'POST':
        username = request.form.get('username')
        password = request.form.get('password')
        # Log the captured credentials for training review (DO NOT store credentials in production)
        print(f"Captured credentials - Username: {username}, Password: {password}")
        message = "This was a simulated phishing attempt. Always verify the URL and authenticity before entering your credentials."
    return f"""
    <html>
        <head>
            <title>Secure Login</title>
        </head>
        <body>
            <h2>Login</h2>
            <form method="post">
                <label for="username">Username:</label>
                <input type="text" id="username" name="username" required><br><br>
                <label for="password">Password:</label>
                <input type="password" id="password" name="password" required><br><br>
                <input type="submit" value="Login">
            </form>
            <p>{message}</p>
        </body>
    </html>
    """

if __name__ == '__main__':
    # Run in debug mode for training purposes on a controlled network
    app.run(debug=True)
```

---

## 3. Vishing Simulation Using Text-to-Speech

This script uses the `pyttsx3` library to simulate a vishing (voice phishing) call by generating a spoken message. It serves as a demonstration of how attackers might use voice tactics to manipulate targets. **Only use this simulation for training exercises.**

> **Installation:**
> ```bash
> pip install pyttsx3
> ```

```python
# vishing_simulation.py
import pyttsx3

def simulate_vishing_call():
    engine = pyttsx3.init()
    message = (
        "Hello, this is a call from your bank's security department. "
        "We have detected suspicious activity on your account. "
        "Please verify your account details immediately by calling our hotline at 1-800-123-4567. "
        "Thank you."
    )
    engine.say(message)
    engine.runAndWait()

if __name__ == '__main__':
    simulate_vishing_call()
```

---

## Final Notes

- **Employee Awareness:** These scripts can be used in training sessions or simulated phishing campaigns (with consent) to educate employees on recognizing and responding to social engineering attempts.
- **Legal and Ethical Use:** Always obtain explicit authorization before conducting any tests or simulations. Ensure all participants are aware that the exercise is for training purposes.
- **Documentation and Feedback:** Use the results from these simulations to provide constructive feedback and improve your organization's security awareness and incident response protocols.

*Happy learning, and remember: understanding social engineering is the first step in building a robust human firewall!*