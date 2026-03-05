

## **Lab Title: Network Security & Firewall Implementation with pfSense**

### **Objective**

To design and deploy a dedicated network security gateway using pfSense. The goal is to establish a secure perimeter between a Wide Area Network (WAN) and a protected Local Area Network (LAN), providing essential services such as firewalling, NAT, and DHCP to internal clients.



### **Tools Used**

* **pfSense CE (Community Edition):** The open-source FreeBSD-based firewall software.
* **VirtualBox/VMware:** To host the virtualized network environment.
* **ISO Image:** pfSense 2.7.2 (or latest stable version).
* **Web Browser:** For accessing the pfSense WebGUI from a client machine.



### **Environment**

* **Hypervisor:** VirtualBox.
* **VM Configuration:** 2 vCPUs, 2GB RAM, 8GB Storage.
* **Network Adapters:**
* **Adapter 1 (WAN):** Bridged Adapter or NAT (to receive internet access).
* **Adapter 2 (LAN):** Internal Network (e.g., "Lab-Net") to serve as the gateway for other VMs.



### **Methodology**

1. **Virtual Machine Setup:** Configured a new VM with two network interfaces to act as the "bridge" between the internet and the internal lab.
2. **Installation:** Booted from the pfSense ISO, partitioned the virtual disk using Auto (ZFS), and performed the standard installation.
3. **Interface Assignment:** * Assigned `vtnet0` to **WAN**.
* Assigned `vtnet1` to **LAN** with a static IP (e.g., `192.168.1.1`).


4. **Client Connection:** Connected a Windows or Kali Linux VM to the same "Internal Network."
5. **WebGUI Configuration:** Accessed the pfSense dashboard via the client’s browser to complete the Setup Wizard, configure DNS, and set administrative credentials.
6. **Rule Validation:** Verified that the LAN client could ping external addresses (DNS/ICMP) while the WAN remained protected from unsolicited inbound traffic.


### **Results**

* **Functional Gateway:** The pfSense firewall successfully provides IP addresses to internal lab machines via DHCP.
* **Traffic Filtering:** Default "Block All" rules are active on the WAN interface, protecting the internal network from external scans.
* **Web Management:** A secure dashboard is accessible for real-time monitoring of traffic logs and system health.


### **Risk Analysis**

| Risk | Impact | Likelihood |
| --- | --- | --- |
| **Weak Admin Credentials** | High | Medium |
| **Unrestricted Outbound Traffic** | Medium | High |
| **Outdated Firmware** | High | Low |



### **Mitigation Recommendations**

* **Access Control:** Change the default `admin` password immediately and consider changing the default WebGUI port (80/443) to a custom port.
* **Egress Filtering:** Implement "Least Privilege" firewall rules to restrict internal machines from communicating over unnecessary ports.
* **Regular Updates:** Check for pfSense security patches monthly to protect against known FreeBSD or PHP vulnerabilities.

## **screenshot**



![WhatsApp Image 2026-02-28 at 15 49 20](https://github.com/user-attachments/assets/70867d30-d51b-409c-9af0-8c18b2dde76c)



![WhatsApp Image 2026-02-28 at 15 49 20 (1)](https://github.com/user-attachments/assets/613e289e-f8a7-4b78-9e73-35688e941892)




![WhatsApp Image 2026-02-28 at 15 49 20 (2)](https://github.com/user-attachments/assets/2172bea4-ef7a-45e3-88e5-eb6ae17c1ed5)

  


![WhatsApp Image 2026-02-28 at 15 49 20 (3)](https://github.com/user-attachments/assets/0971ec87-67e8-43f1-8bc1-c5385a794158)
![WhatsApp Image 2026-02-28 at 15 49 20 (4)](https://github.com/user-attachments/assets/b33b6f18-5a4d-403f-affa-ff581eb0ee7f)


![WhatsApp Image 2026-02-28 at 15 49 20 (5)](https://github.com/user-attachments/assets/9dea6218-6ebe-4b2c-922e-7c5aa2a05171)



![WhatsApp Image 2026-02-28 at 15 49 21](https://github.com/user-attachments/assets/d774a0cd-e358-4e87-838a-562142015468)




![WhatsApp Image 2026-02-28 at 15 49 21 (1)](https://github.com/user-attachments/assets/c5294abe-ff5b-4bd1-a30e-8c3392ac5e7e)



![WhatsApp Image 2026-02-28 at 15 49 21 (2)](https://github.com/user-attachments/assets/08cc242f-0693-4a57-996d-773beb085ae0)



![WhatsApp Image 2026-02-28 at 15 49 21 (3)](https://github.com/user-attachments/assets/1d962459-12b8-450e-8fee-f5686619ff60)






![WhatsApp Image 2026-02-28 at 15 49 21 (4)](https://github.com/user-attachments/assets/50fbaee0-3cbe-4560-9552-5dbd97c3f598)
![WhatsApp Image 2026-02-28 at 15 49 21 (5)](https://github.com/user-attachments/assets/e16a7aca-0c2f-462d-984e-efd20364cbad)

![WhatsApp Image 2026-02-28 at 15 49 21 (6)](https://github.com/user-attachments/assets/c58aa268-031d-4b95-8611-371abf3b86e8)
![WhatsApp Image 2026-03-04 at 16 54 04](https://github.com/user-attachments/assets/82a18db0-670b-45a6-9c17-a7f410ba0ac3)
![WhatsApp Image 2026-03-04 at 16 54 05](https://github.com/user-attachments/assets/6ea3c319-d14e-4288-a601-018c984eb251)



![WhatsApp Image 2026-03-04 at 16 54 05 (1)](https://github.com/user-attachments/assets/5694af56-b610-44eb-a6f5-2ec436476a04)
![WhatsApp Image 2026-03-04 at 16 54 05 (4)](https://github.com/user-attachments/assets/95b98a2f-a20b-4073-924b-48c208480ad4)






![WhatsApp Image 2026-03-04 at 16 54 05 (2)](https://github.com/user-attachments/assets/0c8a58ca-3dbd-4757-a788-8f48893f0101)



![WhatsApp Image 2026-03-04 at 16 54 05 (3)](https://github.com/user-attachments/assets/8919ce16-1de3-49fc-baa6-6908237c8b41)


### **Conclusion**

The successful installation of pfSense transforms a basic lab into a structured security environment. By isolating the internal network behind a robust firewall, this project demonstrates the fundamental principles of perimeter security and network administration required for professional cybersecurity environments.



