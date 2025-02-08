# Example code for module 6

Below are several example scripts designed to illustrate key concepts from **Module 6: Red Team vs. Blue Team – Simulated Cyber Warfare in Action**. These examples are simplified simulations meant for educational purposes in a controlled lab environment. They demonstrate how the offensive (Red Team) and defensive (Blue Team) processes might be modeled, how activities can be logged and monitored, and how post-exercise reporting might be automated.

> **Important:**
> - **Authorization:** Always run these simulations on systems and networks you control or have explicit permission to test.
> - **Simplified Simulation:** Real-world exercises involve far more complexity. These examples serve only as proof-of-concept educational tools.

---

## Example 1: Red Team Reconnaissance Simulation
This Python script simulates a Red Team performing reconnaissance by scanning a target host for open ports using the `python-nmap` library. (You can install it with `pip install python-nmap`.)

```python
# red_team_recon.py
import nmap
import json
import datetime

def perform_scan(target):
    scanner = nmap.PortScanner()
    print(f"[{datetime.datetime.now()}] Starting scan on {target}...")
    scanner.scan(hosts=target, arguments='-sS -p 1-1024')  # SYN scan on ports 1-1024
    results = {}
    for host in scanner.all_hosts():
        results[host] = {
            'hostname': scanner[host].hostname(),
            'state': scanner[host].state(),
            'protocols': {}
        }
        for proto in scanner[host].all_protocols():
            ports = []
            for port in sorted(scanner[host][proto].keys()):
                port_details = {
                    'port': port,
                    'state': scanner[host][proto][port]['state'],
                    'service': scanner[host][proto][port].get('name', '')
                }
                ports.append(port_details)
            results[host]['protocols'][proto] = ports
    return results

def log_results(results, log_file="red_team_scan_log.json"):
    timestamp = datetime.datetime.now().isoformat()
    log_entry = {
        "timestamp": timestamp,
        "results": results
    }
    with open(log_file, "a") as f:
        f.write(json.dumps(log_entry, indent=4))
        f.write("\n")
    print(f"[{timestamp}] Scan results logged to {log_file}")

if __name__ == '__main__':
    target_ip = "192.168.56.101"  # Replace with your target machine's IP (in your lab)
    scan_results = perform_scan(target_ip)
    log_results(scan_results)
```

*What It Does:*
- Scans the target for open ports between 1 and 1024.
- Logs the scan results (including hostname, port status, and service info) into a JSON file with a timestamp.
- Represents the Red Team’s reconnaissance phase.

---

## Example 2: Red Team Exploitation Simulation
This simple script simulates an exploitation attempt by “attacking” a vulnerable service. In a real exercise, this might invoke an exploit module; here, it simply logs a simulated exploit event.

```python
# red_team_exploit.py
import json
import datetime
import random

def simulate_exploit(target, vulnerability):
    # Simulate the success or failure of an exploit
    success = random.choice([True, False])
    event = {
        "timestamp": datetime.datetime.now().isoformat(),
        "target": target,
        "vulnerability": vulnerability,
        "exploit_success": success,
        "details": "Simulated exploitation event."
    }
    return event

def log_exploit(event, log_file="red_team_exploit_log.json"):
    with open(log_file, "a") as f:
        f.write(json.dumps(event, indent=4))
        f.write("\n")
    print(f"[{event['timestamp']}] Exploit event logged: {event}")

if __name__ == '__main__':
    target_ip = "192.168.56.101"  # Replace with your target machine's IP
    vulnerability = "CVE-XXXX-XXXX (Simulated Vulnerability)"
    exploit_event = simulate_exploit(target_ip, vulnerability)
    log_exploit(exploit_event)
```

*What It Does:*
- Simulates an exploit attempt against a given target.
- Randomly marks the exploit as successful or not.
- Logs the simulated event, representing the Red Team’s attempt to breach the target.

---

## Example 3: Blue Team Log Monitoring Simulation
This script simulates the Blue Team monitoring system logs for suspicious events. It reads from a (simulated) log file and raises an alert when it detects indicators of an attack (for example, a successful exploitation event).

```python
# blue_team_monitor.py
import json
import time
import datetime

def monitor_log(log_file="red_team_exploit_log.json"):
    print(f"[{datetime.datetime.now()}] Blue Team monitoring started on {log_file}")
    already_seen = set()
    while True:
        try:
            with open(log_file, "r") as f:
                for line in f:
                    if line.strip():
                        try:
                            event = json.loads(line)
                            event_id = event.get("timestamp")
                            if event_id not in already_seen:
                                already_seen.add(event_id)
                                process_event(event)
                        except json.JSONDecodeError:
                            continue
            time.sleep(5)  # Check the log every 5 seconds
        except FileNotFoundError:
            print(f"Log file {log_file} not found. Waiting for log creation...")
            time.sleep(5)

def process_event(event):
    # For this simulation, raise an alert if an exploit was successful.
    if event.get("exploit_success"):
        print(f"[{event['timestamp']}] ALERT: Successful exploit detected on {event['target']}!")
        # In a real environment, here you might trigger an incident response workflow.
    else:
        print(f"[{event['timestamp']}] Notice: Exploit attempt on {event['target']} failed.")

if __name__ == '__main__':
    monitor_log()
```

*What It Does:*
- Continuously monitors a log file (`red_team_exploit_log.json`) for new entries.
- Processes each event to detect indicators of a successful attack.
- Raises an alert (prints to the console) if a successful exploit is detected—simulating the Blue Team’s real-time detection and response.

---

## Example 4: Combined Simulation – Red and Blue Team Exercise
This example shows a simplified combined exercise. A single script alternates between generating Red Team events (both reconnaissance and exploitation) and a Blue Team process that periodically checks the logs. In practice, these would run on separate systems or processes, but here they are shown sequentially for demonstration.

```python
# red_blue_exercise.py
import threading
import time
import json
import datetime
import random

RED_LOG_FILE = "red_team_exploit_log.json"

# --- Red Team Functions ---
def red_team_recon(target):
    # Simulate a reconnaissance event (here, we just print a message)
    print(f"[{datetime.datetime.now()}] [Red Team] Reconnaissance initiated on {target}.")

def red_team_exploit(target, vulnerability):
    # Simulate an exploit event
    success = random.choice([True, False])
    event = {
        "timestamp": datetime.datetime.now().isoformat(),
        "target": target,
        "vulnerability": vulnerability,
        "exploit_success": success,
        "details": "Simulated exploit during exercise."
    }
    with open(RED_LOG_FILE, "a") as f:
        f.write(json.dumps(event) + "\n")
    print(f"[{event['timestamp']}] [Red Team] Exploit event logged for target {target}.")
    return event

def red_team_activity():
    target = "192.168.56.101"
    vulnerability = "CVE-XXXX-XXXX (Simulated)"
    while True:
        red_team_recon(target)
        time.sleep(3)  # Wait before launching an exploit
        red_team_exploit(target, vulnerability)
        time.sleep(10)  # Pause between cycles

# --- Blue Team Functions ---
def blue_team_monitor():
    already_seen = set()
    while True:
        try:
            with open(RED_LOG_FILE, "r") as f:
                for line in f:
                    if line.strip():
                        try:
                            event = json.loads(line)
                            event_id = event.get("timestamp")
                            if event_id not in already_seen:
                                already_seen.add(event_id)
                                process_blue_event(event)
                        except json.JSONDecodeError:
                            continue
            time.sleep(5)
        except FileNotFoundError:
            time.sleep(5)

def process_blue_event(event):
    if event.get("exploit_success"):
        print(f"[{event['timestamp']}] [Blue Team] ALERT: Successful exploit detected on {event['target']}!")
    else:
        print(f"[{event['timestamp']}] [Blue Team] Notice: Exploit attempt on {event['target']} failed.")

# --- Main Execution ---
if __name__ == '__main__':
    # Start Red Team activity in a separate thread.
    red_thread = threading.Thread(target=red_team_activity, daemon=True)
    red_thread.start()

    # Start Blue Team monitoring in the main thread.
    blue_team_monitor()
```

*What It Does:*
- **Red Team Activity:**
    - Simulates periodic reconnaissance and exploitation events.
    - Logs each exploitation attempt (with random success/failure) to a shared log file.
- **Blue Team Monitoring:**
    - Continuously reads the log file and processes new events.
    - Prints alerts when a successful exploit is detected.
- **Combined Simulation:**
    - Demonstrates a basic feedback loop between offensive actions and defensive monitoring.

---

## Final Notes

These examples illustrate several key aspects of Red Team vs. Blue Team exercises:

- **Offensive (Red Team):**
    - Reconnaissance and exploitation simulations that generate log events.
- **Defensive (Blue Team):**
    - Real-time log monitoring and alerting based on detected events.
- **Integration:**
    - How both teams can be simulated together to create a learning exercise.

In a real-world setting, the tools and techniques would be far more complex, and the teams would use dedicated tools (e.g., Metasploit, SIEM systems, IDS/IPS, etc.). Use these examples as a starting point to understand the dynamics of simulated cyber warfare in an ethical, controlled environment.

Happy simulating, and always practice responsibly with explicit authorization!