Project: Digital Invisible Ink (Steganography Lab)
## Overview
This project explores the art of Steganography—hiding sensitive data inside ordinary-looking files (like images or audio) so that no one even knows a secret message exists. Unlike encryption, which makes a message unreadable, steganography makes the message invisible to the naked eye.

## Objective
The goal of this lab was to demonstrate how "Least Significant Bit" (LSB) insertion works to hide data without altering the visual quality of a carrier file. I aimed to:

Successfully embed a text file into a .jpeg image.

Extract the hidden data without loss of integrity.

Analyze the file's "fingerprint" (hash) before and after to see how the file changed.

## Tools Used
Steghide / OpenStego: Industry-standard tools for embedding and extracting data.

Linux (Kali): The environment used for the exploitation and analysis.

## Steps 
Selected a "Cover Image" with high color complexity to better hide the data.
Create a coverfile using "touch (the name of the file)"
use "echo" to embed the secret message into the file
Then embed the Secret file into the image "steghide --embed -ef (the name of the file) -cf (image downladed)
To extract Use steghide --extract -sf (the saved image ) -xf nowmydata txt

##Screenshot



## Security Implications
Why does this matter to an employer?

Data Exfiltration: Malicious insiders can use steganography to leak company secrets past firewalls that only look for "plain text."

Malware Delivery: Hackers sometimes hide malicious code inside images on a website to bypass antivirus scanners.

Digital Watermarking: On the positive side, it’s used for copyright protection to prove ownership of digital media.

## Key Takeaways
Trust Nothing: Just because a file looks like a "cat photo" doesn't mean it is just a cat photo.

Detection is Hard: Traditional antivirus often misses stego-files; it requires Steganalysis (statistical analysis of file data) to catch.

Layered Defense: Always encrypt data before hiding it. Security should never rely on "secrecy" alone.

## Future Enhancements
Implementing Steganalysis tools (like StegExpose) to see if I can "crack" my own hidden messages.

Automating the process with a Python GUI for easier use.
