

#  Kali Linux Basic Commands Cheat Sheet

This repository contains a categorized list of essential Linux commands used during penetration testing and security auditing in **Kali Linux**.

---

##  1. File & Directory Management

These are the "navigation" commands used to move around the system and manage files.

| Command | Description | Example |
| --- | --- | --- |
| `pwd` | **Print Working Directory**: Shows exactly which folder you are currently in. | `pwd` |
| `ls` | **List**: Shows all files and folders in the current directory. | `ls -la` (shows hidden files) |
| `cd` | **Change Directory**: Moves you into a different folder. | `cd /home/kali/Downloads` |
| `mkdir` | **Make Directory**: Creates a new folder. | `mkdir Lab_Results` |
| `cp` | **Copy**: Copies a file or directory from one place to another. | `cp report.txt /backup/` |
| `mv` | **Move**: Moves or renames a file/folder. | `mv oldname.txt newname.txt` |
| `rm` | **Remove**: Deletes a file. **Use with caution.** | `rm -rf folder_name` (deletes folder) |

---

##  2. System & Permissions

In Cybersecurity, you often need "Root" (Administrator) access to run tools like Nmap or Wireshark.

* **`sudo`**: Stands for "SuperUser Do." It allows you to run a command with administrative privileges.
* **`chmod`**: Changes file permissions. This is vital when you download a script that isn't "executable" yet.
* *Example:* `chmod +x script.py` (Makes the script runnable).


* **`chown`**: Changes the owner of a file.
* **`passwd`**: Allows you to change the password for a user.



##  3. Networking & Reconnaissance

These commands are the bread and butter of your cybersecurity journey.

### **Networking Basics**

* **`ifconfig` / `ip a**`: Displays your IP address and network interface details (Ethernet, Wi-Fi).
* **`ping`**: Checks if a target host is alive and reachable.
* **`netstat -tuln`**: Shows all active ports and connections on your own machine.

### **Primary Recon Tools**

* **`nmap`**: The industry standard for network discovery and security auditing.
* *Example:* `nmap -sV <IP>` (Detects versions of services).


* **`whois`**: Look up domain registration information to find ownership details.
* **`dig` / `nslookup**`: Used to query DNS servers for records (A, MX, TXT).

---

##  4. Text Manipulation & Searching

Security analysts often have to search through massive "Log Files" to find a single line of suspicious activity.

* **`cat`**: Displays the entire content of a file on your screen.
* **`grep`**: Search for a specific word or pattern inside a file.
* *Example:* `cat access.log | grep "failed"` (Finds all failed login attempts).


* **`head` / `tail**`: Shows only the first or last few lines of a file.
* *Example:* `tail -f /var/log/apache2/access.log` (Watch web traffic in real-time).


* **`nano` / `vim**`: Text editors used to write scripts or edit configuration files within the terminal.

---

##  5. Package Management

Keeping Kali updated is essential to ensure you have the latest exploit signatures.

* **`apt update`**: Updates the list of available packages.
* **`apt upgrade`**: Installs the actual updates.
* **`apt install <tool>`**: Downloads and installs a new security tool.
* *Example:* `sudo apt install gobuster`



