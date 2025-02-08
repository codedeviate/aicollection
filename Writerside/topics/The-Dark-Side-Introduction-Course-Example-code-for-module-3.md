# Example code for module 3

Below are several code examples that illustrate how you might leverage and integrate some of the essential penetration testing tools discussed in **Module 3: Tools of the Trade – A Comprehensive Guide to Penetration Testing Tools**. These examples are provided for educational purposes only and should be used in controlled, authorized environments. In many cases, we use Python (or other languages) to automate or interface with these tools.

---

## 1. Reconnaissance and Information Gathering with Nmap

**Overview:**  
Nmap is widely used for host discovery, port scanning, and service/OS detection. The following Python script uses the [python‑nmap](https://pypi.org/project/python-nmap/) library to perform a scan on a subnet.

> **Installation:**
> ```bash
> pip install python-nmap
> ```

```python
# nmap_scan.py
import nmap

def scan_network(target):
    scanner = nmap.PortScanner()
    # -sV for service/version detection, -O for OS detection
    scanner.scan(hosts=target, arguments='-sV -O')
    results = {}
    for host in scanner.all_hosts():
        host_info = {
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
            host_info['protocols'][proto] = ports
        results[host] = host_info
    return results

if __name__ == '__main__':
    target_subnet = '192.168.1.0/24'  # Change to your authorized target
    scan_results = scan_network(target_subnet)
    for host, info in scan_results.items():
        print(f"Host: {host} ({info['hostname']})")
        print(f"  State: {info['state']}")
        for proto, ports in info['protocols'].items():
            print(f"  Protocol: {proto}")
            for port in ports:
                print(f"    Port {port['port']} - {port['state']} ({port['service']})")
```

---

## 2. Vulnerability Assessment with OpenVAS (GVM)

**Overview:**  
OpenVAS (now part of the Greenbone Vulnerability Management suite) automates vulnerability scanning. While OpenVAS is primarily managed via a web interface, you can also interact with it using Python. For example, the [python-gvm](https://github.com/greenbone/python-gvm) library enables you to communicate with the Greenbone Management Protocol (GMP).

> **Note:** The snippet below is a simplified example. In real deployments, you would use proper authentication, handle exceptions, and work with scan tasks and reports.
>
> **Installation:**
> ```bash
> pip install python-gvm
> ```

```python
# openvas_scan.py
from gvm.connections import UnixSocketConnection  # or use TCPConnection for remote hosts
from gvm.protocols.gmp import Gmp

def list_tasks():
    connection = UnixSocketConnection()  # Adjust connection type and parameters as needed
    with Gmp(connection=connection) as gmp:
        gmp.authenticate('admin', 'yourpassword')  # Replace with your credentials
        tasks = gmp.get_tasks()
        for task in tasks.xpath('//task'):
            name = task.xpath('name/text()')[0]
            status = task.xpath('status/text()')[0]
            print(f"Task: {name}, Status: {status}")

if __name__ == '__main__':
    list_tasks()
```

---

## 3. Exploitation Framework with Metasploit

**Overview:**  
Metasploit’s powerful exploitation framework can be automated using its RPC API. The [python‑msfrpc](https://github.com/rapid7/metasploit-framework/wiki/Msfrpc) (or similar) library lets you connect to Metasploit, search for exploits, and even launch modules from a Python script.

> **Note:** Ensure that the Metasploit RPC daemon is running and that you have the proper permissions before executing exploits.
>
> **Installation:**  
> You may need to install a compatible msfrpc library or use the built‑in RPC client (versions and libraries may vary).

```python
# metasploit_example.py
# This example uses the MsfRpcClient from the metasploit.msfrpc package.
# Make sure to run msfrpcd or use msfconsole with RPC enabled.

try:
    from metasploit.msfrpc import MsfRpcClient
except ImportError:
    print("Please install the msfrpc client library.")
    exit(1)

def search_exploits(keyword):
    client = MsfRpcClient('your_password', server='127.0.0.1', port=55553)  # adjust port and password as needed
    # Search for exploits related to the keyword (e.g., 'ftp')
    exploits = client.modules.exploits.search(keyword)
    print(f"Exploits matching '{keyword}':")
    for mod in exploits:
        print(mod)

if __name__ == '__main__':
    search_exploits('ftp')
```

---

## 4. Web Application Testing with Burp Suite Extension

**Overview:**  
Burp Suite is a comprehensive web application testing platform. You can extend its functionality with custom extensions written in Jython (Python running on the Java Virtual Machine). The sample below logs every HTTP request URL that passes through Burp’s proxy.

> **Usage:**  
> Save the code as a Jython script (e.g., `burp_extender.py`) and load it into Burp Suite via the Extender tab.
>
> **Note:** This script must be run with Burp’s bundled Jython interpreter.

```python
# burp_extender.py
from burp import IBurpExtender, IHttpListener

class BurpExtender(IBurpExtender, IHttpListener):
    def registerExtenderCallbacks(self, callbacks):
        self._callbacks = callbacks
        self._helpers = callbacks.getHelpers()
        callbacks.setExtensionName("Simple Request Logger")
        callbacks.registerHttpListener(self)
        print("Burp Extension Loaded: Simple Request Logger")
        return

    def processHttpMessage(self, toolFlag, messageIsRequest, messageInfo):
        if messageIsRequest:
            request = messageInfo.getRequest()
            analyzedRequest = self._helpers.analyzeRequest(request)
            url = analyzedRequest.getUrl()
            print("HTTP Request URL: " + str(url))
```

---

## 5. Network Analysis with Wireshark using PyShark

**Overview:**  
Wireshark is excellent for network traffic analysis. [PyShark](https://github.com/KimiNewt/pyshark) is a Python wrapper for tshark (Wireshark’s command‑line tool) that allows you to capture and analyze network packets in real time.

> **Installation:**
> ```bash
> pip install pyshark
> ```
>
> **Note:** Running live captures requires appropriate permissions on your network interface.

```python
# pyshark_capture.py
import pyshark

def capture_http_packets(interface='eth0', packet_count=5):
    # Capture live packets on the specified interface with an HTTP filter
    capture = pyshark.LiveCapture(interface=interface, display_filter='http')
    print(f"Capturing {packet_count} HTTP packets on interface {interface}...")
    for packet in capture.sniff_continuously(packet_count=packet_count):
        try:
            # Display source, destination, and HTTP host if available
            src = packet.ip.src
            dst = packet.ip.dst
            http_host = packet.http.host if hasattr(packet, 'http') else 'N/A'
            print(f"Packet from {src} to {dst}, HTTP Host: {http_host}")
        except AttributeError:
            # Some packets might not have the expected attributes
            continue

if __name__ == '__main__':
    capture_http_packets(interface='eth0', packet_count=5)
```

---

## 6. Post-Exploitation Reporting: Generating a JSON Report

**Overview:**  
After testing, it’s essential to compile your findings in a clear, structured report. The following Python script demonstrates how to aggregate dummy scan and exploitation results into a JSON report.

```python
# generate_report.py
import json

def generate_report(nmap_results, metasploit_results):
    report = {
        "nmap": nmap_results,
        "metasploit": metasploit_results,
        "summary": "Comprehensive penetration testing report. Findings from reconnaissance and exploitation phases."
    }
    with open('pentest_report.json', 'w') as f:
        json.dump(report, f, indent=4)
    print("Report saved as pentest_report.json")

if __name__ == '__main__':
    # Sample dummy data representing results from previous phases
    nmap_results = {
        "192.168.1.101": {
            "hostname": "target-host",
            "state": "up",
            "protocols": {
                "tcp": [{"port": 22, "state": "open", "service": "ssh"},
                        {"port": 80, "state": "open", "service": "http"}]
            }
        }
    }
    metasploit_results = {
        "exploits_found": ["exploit/unix/ftp/vsftpd_234_backdoor", "exploit/multi/http/struts2_content_type_ognl"]
    }
    generate_report(nmap_results, metasploit_results)
```

---

## Final Notes

These examples demonstrate how to integrate some of the key penetration testing tools into a cohesive workflow:

- **Reconnaissance:** Use Python and Nmap for host and service discovery.
- **Vulnerability Assessment:** Interface with OpenVAS (GVM) to manage and view scan tasks.
- **Exploitation:** Leverage Metasploit’s RPC API to search for and, in controlled labs, execute exploits.
- **Web Testing:** Extend Burp Suite with a custom Jython extension to monitor HTTP traffic.
- **Network Analysis:** Use PyShark to capture and analyze live network traffic.
- **Reporting:** Combine scan and exploitation results into a structured JSON report.

Always ensure you have explicit authorization before testing any system, and use these tools responsibly within legal and ethical boundaries. Happy testing, and keep learning!