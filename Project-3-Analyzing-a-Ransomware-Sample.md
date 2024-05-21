# Analyzing a Ransomware Sample

## Introduction
Ransomware is a type of malware that encrypts a victim's files and demands payment for the decryption key. Understanding how ransomware operates can help in developing strategies to defend against it and respond to incidents. In this project, you will analyze a ransomware sample to understand its encryption mechanism, ransom note delivery, and other behaviors.

## Pre-requisites
- Basic understanding of malware and its types, particularly ransomware.
- Familiarity with Windows operating system internals.
- Knowledge of encryption basics.
- Familiarity with dynamic analysis tools.

## Lab Set-up
1. Operating System: Use a Windows virtual machine (VM) created using VirtualBox or VMware.
2. Ransomware Sample: Obtain a known and safe-to-analyze ransomware sample from a reputable source like MalwareBazaar.
3. Tools:
  - Procmon (Process Monitor): For monitoring file system, registry, and process/thread activity.
  - Wireshark: For capturing and analyzing network traffic.
  - RegShot: For comparing registry snapshots.
  - FakeNet-NG: For simulating network services to capture malware communication.
  - HxD (Hex Editor): For examining binary data.
  - AES Crypt: For testing encryption mechanisms.
Ensure your VM is isolated from your main network and has a snapshot taken before analysis to easily revert to a clean state.

## Exercise: Analyzing the Encryption Mechanism of the Ransomware
Objective: Execute the ransomware sample in a controlled environment to understand its encryption mechanism and analyze its behavior, including file encryption and ransom note delivery.

Step 1: Set Up the Environment:

- Ensure the VM is isolated from your main network.
- Install and configure the necessary tools: Procmon, Wireshark, RegShot, and FakeNet-NG.
- Take a snapshot of the VM for easy restoration.

Step 2: Initial Snapshot:

- Use RegShot to take an initial snapshot of the registry.
- Create some test files (e.g., text documents, images) to observe encryption.

Step 3: Execute the Ransomware Sample:

- Start Procmon to begin monitoring.
- Execute the ransomware sample within the VM.
- Observe and record the behavior of the ransomware in real-time.

Step 4: Collect Data:

- Let the ransomware run until it completes its encryption process and displays a ransom note.
- Stop Procmon and save the captured events log.
- Use Wireshark to capture network traffic during the execution.

Step 5: Analyze the Collected Data:

- File System Activity: In Procmon, filter events to focus on file system activity. Identify files that were encrypted by the ransomware.
- Registry Activity: Filter events to examine registry changes. Look for new keys, modified values, or deleted entries.
- Encryption Analysis: Identify the encryption algorithm used by examining encrypted files and comparing them to their original versions.

Step 6: Post-execution Snapshot:

- Use RegShot to take a second snapshot of the registry.
- Compare the two snapshots to identify changes made by the ransomware.

# Expected Output

- File System Activity: In Procmon, you might observe the ransomware encrypting files in user directories and appending a specific extension to them. Example findings:

```
Modified: C:\Users\Public\Documents\example.txt -> C:\Users\Public\Documents\example.txt.encrypted
Created: C:\Users\Public\Documents\READ_ME.txt (ransom note)
```

- Registry Activity: You may find the ransomware adding new registry entries to establish persistence or modifying existing keys to alter system behavior. Example findings:

```
Added: HKCU\Software\Ransomware\EncryptedFiles
Modified: HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters
```

- Encryption Analysis:

- Compare the encrypted files with the original versions to identify the encryption algorithm. You might use tools like HxD to look for patterns in the encrypted data.
- If the ransomware uses a known encryption algorithm (e.g., AES), you may identify typical characteristics such as block size and structure. Example analysis:
```
Original file size: 1 KB
Encrypted file size: 1 KB (indicating block cipher)
Hex pattern analysis: Encrypted data does not show simple repeating patterns, indicating strong encryption.
```
- Ransom Note Analysis: Examine the ransom note file (READ_ME.txt) created by the ransomware. It typically contains instructions for payment and may include a contact email or a URL for payment.


By completing this exercise, you will gain practical experience in analyzing ransomware, understanding its encryption mechanisms, and identifying how it demands ransom from victims. This knowledge is crucial for developing effective defense and response strategies against ransomware attacks.







