
# Lab: File System Manipulation & Data Management in Kali Linux

## 1. Objective
The goal of this lab was to demonstrate proficiency in the **Linux Command Line Interface (CLI)** by creating, organizing, and managing multiple files and directories. Mastering these commands is a prerequisite for security analysts to manage logs, automate outputs, and organize evidence during an investigation.


## 2. Tools & Environment
* **Operating System:** Kali Linux (Virtual Machine)
* **Terminal:** ZSH/Bash
* **Primary Commands:** `mkdir`, `touch`, `echo`, `ls`



## 3. Methodology
I performed a series of tasks to simulate the organization of a penetration testing project:

**Commands Executed:**
bash
# Create a dedicated lab directory
mkdir -p ~/Labs/FileManagement && cd ~/Labs/FileManagement

# Create 10 files at once for log simulation
touch pilot_{1..10}.txt

# Write a secret key to one file using redirection
echo "we have 3 pilot" > pilot.txt



**Lab Screenshot:**
<img width="637" height="511" alt="Screenshot 2026-02-24 120246" src="https://github.com/user-attachments/assets/439d0b51-ed49-4204-ae3f-ed03036586e1" />



## 4. Results

| Task | Command Used | Result |

| **Create Folder** | `mkdir` | Successfully created a structured lab environment. |

| **Batch Creation** | `touch {1..10}` | Generated 10 unique files in under 1 second. |

| **File Editing** | `echo >` | Populated files with sensitive data for testing. |

| **Audit** | `ls -lh` | Verified all files exist with correct sizes and metadata. |



## 5. Risk Analysis

In a real-world security environment, improper file management leads to several risks:

* **Data Leakage:** Leaving sensitive information in plain text without proper permissions.
* **Log Tampering:** Attackers can use `echo` or `rm` to overwrite or delete logs to hide their tracks.
* **Information Overload:** Creating thousands of files via automation can lead to "Zip Bombs" or Disk Exhaustion (Denial of Service).



## 6. Mitigation Recommendations

1. **Permission Hardening:** Use `chmod 600` on sensitive files so only the owner can read or write to them.
2. **Encryption:** Never store passwords in plain text; use tools like `GnuPG` to encrypt sensitive evidence files.
3. **Immutable Logs:** Configure system logs to be "append-only" using `chattr +a` so that existing data cannot be deleted.


## 7. Conclusion

This lab confirms my ability to navigate and manipulate the Linux backend efficiently. While seemingly simple, the ability to rapidly create and modify files is a prerequisite for **Bash Scripting** and **Incident Response**. By understanding how files are managed in the terminal, I am better equipped to detect unauthorized file changes during a security investigation.

`

