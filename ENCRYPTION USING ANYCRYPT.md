

# **🛡️ Project: Universal Data Encryption (AnyCript Lab)**
## Overview
In this lab, I used AnyCript, a multi-functional digital toolbox, to secure sensitive information using industry-standard algorithms. I focused on implementing AES (Advanced Encryption Standard) to protect text-based data.

## Objective
The goal was to simulate a "Zero-Trust" data environment by:

Transforming human-readable text (plaintext) into secure, unreadable data (ciphertext).

Generating SHA-256 hashes to create unique "digital fingerprints" for data integrity.

Demonstrating the differences between standard encryption and legacy systems like DES.

## Tools Used
AnyCript (Web Toolbox): Used for AES encryption, RSA verification, and SHA-256 hashing.


Text Editor: For preparing the plaintext messages before encryption.

## Steps Taken
Preparation: Drafted a sample "confidential" document containing dummy login credentials.

AES Encryption: Input the plaintext into the AES tool, selected a strong 128-bit or 256-bit key, and generated the ciphertext.

Base64 Encoding: Converted the scrambled ciphertext into Base64 to ensure it remains stable when being pasted into different file types or platforms.

Decryption & Verification: Reversed the process by inputting the key into the decryption module and compared the final result with the original text to ensure 100% accuracy.

## **Screenshots**



<img width="516" height="50" alt="Screenshot 2026-02-12 135559" src="https://github.com/user-attachments/assets/118c53f1-db18-4c38-8a6d-5c8eb5972cce" />



<img width="1299" height="772" alt="Screenshot 2026-02-12 135655" src="https://github.com/user-attachments/assets/ce752f8f-fed3-47b2-ac62-b1776e85043e" />


<img width="1274" height="799" alt="Screenshot 2026-02-12 135722" src="https://github.com/user-attachments/assets/136a3d69-45f0-452e-a1c2-a44db54808cc" />



<img width="1253" height="733" alt="Screenshot 2026-02-12 135817" src="https://github.com/user-attachments/assets/17cab8e4-014c-4904-84b2-1f98571ac2c2" />


## Security Implications
Confidentiality: This process ensures that if a data leak occurs, the stolen files are useless to unauthorized users without the specific key.

Integrity Checks: Using hashing tools prevents "Man-in-the-Middle" attacks where a hacker might try to modify a message while it is being sent.

Cloud Security: Even when using web tools, practicing "Client-Side" habits (like never reusing keys) is vital for organizational safety.

## Key Takeaways
Standardization is Key: I chose AES because it is endorsed by NIST and is the global standard for securing banking and government data.

Tool Versatility: Using a tool like AnyCript shows the importance of having a "utility belt" approach to cybersecurity—being able to convert, merge, and secure data in one workflow.

Human Error: The biggest security risk is often the password/key itself; a strong, 16+ character key is the bare minimum for real protection.

