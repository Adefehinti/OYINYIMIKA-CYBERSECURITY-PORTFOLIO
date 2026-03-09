

## **Lab Title: Deployment and Traffic Analysis of a Cowry SSH Honeypot**

### **Objective**

The objective of this lab is to deploy a **Cowry** medium-interaction honeypot to capture and analyze unauthorized SSH access attempts. The project focuses on setting up a simulated environment to observe brute-force attacks and perform deep packet inspection of the resulting network traffic.

### **Tools Used**

* **Cowry (v2.9.13):** An asynchronous SSH honeypot used to log attacker interaction and keystrokes.
* **Python 3.12.3:** The environment used to run the honeypot within a virtual environment (`cowrie-env`).
* **Wireshark:** Used for network traffic analysis and protocol validation.
* **Nmap:** Utilized for service verification to ensure the honeypot correctly emulates a vulnerable server.
* **VMware Workstation:** The hypervisor hosting the lab infrastructure.

### **Environment**

* **Honeypot Host:** Linux system (Ubuntu/Debian) running on VMware.
* **Attacker Host:** Kali Linux (IP: `192.168.124.128`).
* **Target IP:** `192.168.124.137`.
* **Network Configuration:** The honeypot listens on port **2222**, emulating an OpenSSH 9.2p1 Debian server.

### **Methodology**

1. **Environment Preparation:** Created a Python virtual environment and upgraded `pip` to version 26.0.1 to manage dependencies.
2. **Service Installation:** Installed necessary Python libraries, including `twisted`, `cryptography`, and `bcrypt`, to support the Cowry engine.
3. **Service Verification:** Executed an Nmap scan (`nmap -A`) against the target, which successfully identified the honeypot as an active SSH service.
4. **Attack Simulation:** Initiated connection attempts from the Kali Linux machine to trigger logging and traffic capture.
5. **Traffic Analysis:** Captured packets using Wireshark to inspect the SSHv2 protocol exchange and TCP handshake.
6. **Log Examination:** Analyzed `cowrie.log` and `cowrie.json` to verify the sensor was correctly recording session data.

### **Results**

* **Successful Emulation:** Nmap correctly identified the service as "OpenSSH 9.2p1 Debian 2+deb12u3" on port 2222.
* **Protocol Validation:** Wireshark captures confirmed a successful SSHv2 handshake and identified the specific client and server protocol strings.
* **Data Collection:** The Cowry output engine successfully initialized with a unique Sensor UUID, confirming it was ready to log structured JSON data.

## **screenshot**



<img width="804" height="578" alt="Screenshot 2026-03-05 130638" src="https://github.com/user-attachments/assets/1fd4f744-5838-40af-916e-fc616268cf9b" />






<img width="803" height="579" alt="Screenshot 2026-03-05 131105" src="https://github.com/user-attachments/assets/dd3656e1-ee9e-4159-9567-d2fd0bf12636" />





<img width="812" height="104" alt="Screenshot 2026-03-05 131327" src="https://github.com/user-attachments/assets/43ef404a-35a0-417e-85f4-2b2e83a47128" />




<img width="640" height="405" alt="Screenshot 2026-03-05 132852" src="https://github.com/user-attachments/assets/f93adcdf-b1fc-450e-8038-ec62afe5e57c" />




<img width="616" height="245" alt="Screenshot 2026-03-05 133428" src="https://github.com/user-attachments/assets/688e67e9-e454-4e9c-a56e-aca503961d9f" />




<img width="1718" height="727" alt="Screenshot 2026-03-05 134315" src="https://github.com/user-attachments/assets/84ca8405-8fd6-475d-96a9-cfe0eadcdcc1" />




<img width="1716" height="685" alt="Screenshot 2026-03-05 134701" src="https://github.com/user-attachments/assets/9cd43e0a-b044-467a-8482-0114fd7492e7" />




<img width="805" height="573" alt="Screenshot 2026-03-05 140648" src="https://github.com/user-attachments/assets/fbdfdabb-8fb4-4181-a857-2fbc8ca76263" />











### **Risk Analysis**

* **Detection Risk:** Advanced attackers may recognize port 2222 as a common honeypot port if traffic is not properly redirected.
* **Fingerprinting:** Some automated scanners can identify Cowry-specific responses if the default configuration is not hardened.

### **Mitigation Recommendation**

* **Port Masking:** Use `iptables` to redirect traffic from port 22 to port 2222, making the trap appear more authentic to standard scanners.
* **Filesystem Hardening:** Customize the honeypot’s virtual filesystem (`honeyfs`) to include unique files that match a realistic production server.

### **Conclusion**

This lab successfully demonstrates the implementation of a medium-interaction honeypot. By combining service emulation with deep packet analysis, the setup provides a robust platform for gathering threat intelligence and understanding the initial stages of an SSH-based compromise.
