# Project 4: Behavioral Analysis of a Keylogger

## Introduction
Keyloggers are a type of malware that records keystrokes to capture sensitive information, such as passwords and personal messages. Understanding how keyloggers operate is crucial for detecting and mitigating their impact. In this project, you will analyze a keylogger sample to observe its behavior, including how it captures and stores keystrokes.

## Pre-requisites
- Basic understanding of malware and its types, particularly keyloggers.
- Familiarity with Windows operating system internals.
- Knowledge of system monitoring and analysis tools.
- Understanding of virtual machines and their configuration.

## Lab Set-up
1. Operating System: Use a Windows virtual machine (VM) created using VirtualBox or VMware.
2. Keylogger Sample: Obtain a known and safe-to-analyze keylogger sample from a reputable source like MalwareBazaar.
3. Tools:
  - Procmon (Process Monitor): For monitoring file system, registry, and process/thread activity.
  - Wireshark: For capturing and analyzing network traffic.
  - RegShot: For comparing registry snapshots.
  - Sysinternals Autoruns: For examining startup entries.
  - Text Editor: For examining log files created by the keylogger.
Ensure your VM is isolated from your main network and has a snapshot taken before analysis to easily revert to a clean state.

## Exercise: Monitoring Keystroke Logging Activity
Objective: Execute the keylogger sample in a controlled environment and use Process Monitor to observe its behavior, including how it captures keystrokes and where it stores the logged data.

Step 1: Set Up the Environment:
- Ensure the VM is isolated from your main network.
- Install and configure the necessary tools: Procmon, Wireshark, RegShot, and Sysinternals Autoruns.
- Take a snapshot of the VM for easy restoration.

Step 2: Initial Snapshot:

- Use RegShot to take an initial snapshot of the registry.

Step 3: Execute the Keylogger Sample:

- Start Procmon to begin monitoring.
- Execute the keylogger sample within the VM.
- Perform typical user activities (e.g., typing in a text editor) to generate keystroke data.
  
Step 4: Collect Data:

- Let the keylogger run for a few minutes, capturing keystrokes.
- Stop Procmon and save the captured events log.

Step 5: Analyze the Collected Data:

- File System Activity: In Procmon, filter events to focus on file system activity. Identify any files created or modified by the keylogger, particularly those that might store logged keystrokes.
- Registry Activity: Filter events to examine registry changes. Look for new keys or modified values associated with the keylogger.
- Process and Thread Activity: Check for any processes or threads spawned by the keylogger.
- Log File Analysis: Locate and examine any log files to understand the format and content of captured keystrokes.

Step 6: Post-execution Snapshot:

- Use RegShot to take a second snapshot of the registry.
- Compare the two snapshots to identify changes made by the keylogger.

## Expected Solution/Output

- File System Activity: In Procmon, you might observe the keylogger creating or modifying log files in user directories. Example findings:

```
Created: C:\Users\Public\Documents\keylog.txt
Modified: C:\Users\Public\Documents\keylog.txt
```

- Registry Activity: You may find the keylogger adding new registry entries to establish persistence. Example findings:

```
Added: HKCU\Software\Microsoft\Windows\CurrentVersion\Run\Keylogger
Modified: HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System
```

- Process and Thread Activity: The keylogger might spawn new processes or inject code into existing ones to monitor keystrokes. Example findings:

```
Created: Process PID 5678 (keylogger.exe)
Injected: Thread into explorer.exe
```

- Log File Analysis: Locate the log file (e.g., keylog.txt) and examine its content. You may find captured keystrokes and possibly timestamps indicating when each keystroke was logged. Example findings:

```
[2024-05-17 10:15:00] Username: JohnDoe
[2024-05-17 10:15:05] Password: mypassword123
```
By completing this exercise, you will gain practical experience in analyzing keylogger behavior, understanding how they capture and store keystrokes, and identifying persistence mechanisms. This knowledge is crucial for detecting and mitigating keylogger infections effectively.
