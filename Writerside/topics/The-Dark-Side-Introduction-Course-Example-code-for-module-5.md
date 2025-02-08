# Example code for module 5

Below are several code examples designed to support the concepts in **Module 5: Building Your Own Ethical Hacking Lab – A Step-by-Step Guide**. These examples help automate common lab setup tasks and testing within your controlled, isolated environment. **Always use these examples on systems you own or on lab networks where you have explicit permission.**

---

## Example 1: Vagrantfile for Setting Up Your Ethical Hacking Lab

This Vagrantfile sets up a simple lab with two virtual machines on a private network: one for your penetration testing platform (using Kali Linux) and one as a vulnerable target (using Ubuntu). You can use VirtualBox (or another provider) to run these VMs.

> **Prerequisites:**
> - Install [Vagrant](https://www.vagrantup.com/) and [VirtualBox](https://www.virtualbox.org/).
> - Ensure you have an internet connection to download the base boxes.

```ruby
# Vagrantfile
Vagrant.configure("2") do |config|
  # Kali Linux Penetration Testing VM
  config.vm.define "kali" do |kali|
    kali.vm.box = "kalilinux/rolling"
    kali.vm.hostname = "kali-lab"
    kali.vm.network "private_network", ip: "192.168.56.10"
    kali.vm.provider "virtualbox" do |vb|
      vb.memory = "2048"
      vb.cpus = 2
    end
    kali.vm.provision "shell", inline: <<-SHELL
      echo "Updating Kali Linux..."
      sudo apt update && sudo apt upgrade -y
      echo "Installing additional tools..."
      sudo apt install -y burpsuite wireshark metasploit-framework
    SHELL
  end

  # Vulnerable Target VM (Simulated)
  config.vm.define "vuln" do |vuln|
    vuln.vm.box = "ubuntu/bionic64"
    vuln.vm.hostname = "vuln-target"
    vuln.vm.network "private_network", ip: "192.168.56.11"
    vuln.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
      vb.cpus = 1
    end
    vuln.vm.provision "shell", inline: <<-SHELL
      echo "Setting up the vulnerable target..."
      sudo apt update && sudo apt upgrade -y
      # Here you could simulate vulnerabilities by misconfiguring services or installing outdated packages.
      echo "This system is intentionally left with vulnerable configurations for testing purposes."
    SHELL
  end
end
```

*Usage:*  
Run `vagrant up` in the directory containing this Vagrantfile. This will download the necessary images, create the VMs, and configure them on a private network so that they can communicate with one another.

---

## Example 2: Bash Script to Update and Configure Your Kali Linux VM

This shell script automates the process of updating the Kali Linux system and installing a set of additional penetration testing tools. You can run it on your Kali VM to ensure your lab environment is current.

```bash
#!/bin/bash
# update_kali.sh
# This script updates the Kali Linux system and installs additional tools.

echo "Starting system update..."
sudo apt update && sudo apt upgrade -y

echo "Installing additional penetration testing tools..."
sudo apt install -y burpsuite wireshark metasploit-framework

echo "System update and tool installation complete."
```

*Usage:*  
Save the script as `update_kali.sh`, make it executable with `chmod +x update_kali.sh`, then run it using `./update_kali.sh`.

---

## Example 3: Bash Script to Take a Snapshot of a VirtualBox VM

Before performing major tests or experiments, it’s good practice to take a snapshot of your VM. This script uses VirtualBox’s command-line tool (`VBoxManage`) to create a snapshot of a specified VM.

```bash
#!/bin/bash
# snapshot_lab.sh
# This script takes a snapshot of a specified VirtualBox VM.

# Replace "kali-lab" with the exact name of your VM as recognized by VirtualBox.
VM_NAME="kali-lab"
SNAPSHOT_NAME="pre_experiment_snapshot"

echo "Taking snapshot of VM: $VM_NAME..."
VBoxManage snapshot "$VM_NAME" take "$SNAPSHOT_NAME" --pause

if [ $? -eq 0 ]; then
  echo "Snapshot '$SNAPSHOT_NAME' taken successfully."
else
  echo "Failed to take snapshot. Please check the VM name and try again."
fi
```

*Usage:*  
Save the script as `snapshot_lab.sh`, give it executable permissions (`chmod +x snapshot_lab.sh`), and run it from the command line.

---

## Example 4: Python Script to Test Connectivity Between Lab Machines

This Python script checks connectivity between your lab VMs by pinging their IP addresses. It’s a simple way to ensure that your network configuration is correct.

```python
# connectivity_check.py
import subprocess

def ping_host(host):
    try:
        # Use the "-c 4" flag for Unix-based systems; adjust if using Windows.
        output = subprocess.check_output(["ping", "-c", "4", host], stderr=subprocess.STDOUT, universal_newlines=True)
        print(f"Host {host} is reachable:")
        print(output)
    except subprocess.CalledProcessError as e:
        print(f"Failed to reach {host}:")
        print(e.output)

if __name__ == '__main__':
    # IP addresses should match those configured in your Vagrantfile.
    hosts = ["192.168.56.10", "192.168.56.11"]
    for host in hosts:
        ping_host(host)
```

*Usage:*  
Run the script with `python3 connectivity_check.py` to see the ping results from each host.

---

## Final Notes

These code examples provide practical steps to help you build and manage your own ethical hacking lab:

- **Vagrantfile:** Quickly sets up a multi-VM lab environment.
- **Bash Scripts:** Automate system updates, tool installations, and snapshot management.
- **Python Script:** Verifies network connectivity within your lab.

By following these examples and tailoring them to your specific needs, you’ll create a safe, controlled environment to practice penetration testing and further develop your ethical hacking skills. Remember to always work within authorized, legal, and isolated environments.

Happy lab building, and keep learning!