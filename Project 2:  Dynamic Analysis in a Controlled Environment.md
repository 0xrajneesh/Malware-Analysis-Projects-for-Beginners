# Dynamic Analysis in a Controlled Environment

## Introduction
Dynamic analysis involves executing malware in a controlled and isolated environment to observe its behavior. This approach allows you to monitor how the malware interacts with the system, such as file modifications, network communications, and changes to the registry. In this project, you will perform dynamic analysis on a simple malware sample to understand its operational characteristics.

## Pre-requisites
- Basic understanding of malware and its types.
- Familiarity with Windows operating system internals.
- Understanding of virtual machines and their configuration.
- Knowledge of networking and system monitoring tools.

## Lab Set-up
1. Operating System: Use a Windows virtual machine (VM) created using VirtualBox or VMware.
2. Malware Sample: Obtain a known and safe-to-analyze malware sample from a reputable source like MalwareBazaar.
3. Tools:
- Procmon (Process Monitor): For monitoring file system, registry, and process/thread activity.
- Wireshark: For capturing and analyzing network traffic.
- RegShot: For comparing registry snapshots.
- FakeNet-NG: For simulating network services to capture malware communication.

Ensure your VM is isolated from your main network and has a snapshot taken before analysis to easily revert to a clean state.

## Exercise: Monitoring Malware Behavior with Process Monitor
Objective: Execute the malware sample in a controlled environment and use Process Monitor to observe its behavior, including file, registry, and process activity.

Step 1: Set Up the Environment

- Ensure the VM is isolated from your main network.
- Install and configure the necessary tools: Procmon, Wireshark, RegShot, and FakeNet-NG.
- Take a snapshot of the VM for easy restoration.

Step 2: Initial Snapshot

- Use RegShot to take an initial snapshot of the registry.
- Run FakeNet-NG to simulate network services.

Step 3: Execute the Malware Sample

- Start Procmon to begin monitoring.
- Execute the malware sample within the VM.
- Observe and record the behavior of the malware in real-time.

Step 4: Collect Data:

- Let the malware run for a few minutes, capturing all activities with Procmon.
- Stop Procmon and save the captured events log.
- Use Wireshark to capture network traffic during the execution.

Step 5: Analyze the Collected Data

- File System Activity: In Procmon, filter events to focus on file system activity. Identify files created, modified, or deleted by the malware.
- Registry Activity: Filter events to examine registry changes. Look for new keys, modified values, or deleted entries.
- Process and Thread Activity: Check for new processes or threads spawned by the malware.
- Network Activity: Analyze Wireshark captures to identify communication attempts, such as connecting to external IP addresses or domains.

Step 6: Post-execution Snapshot

- Use RegShot to take a second snapshot of the registry.
- Compare the two snapshots to identify changes made by the malware.

## Expected Output

- File System Activity: In Procmon, you might observe the malware creating or modifying files in the system directory or user profile folders. Example findings:

```
Created: C:\Users\Public\malicious_file.exe
Modified: C:\Windows\System32\drivers\etc\hosts

```
- Registry Activity: You may find the malware adding new registry entries to establish persistence or modify existing keys to alter system behavior. Example findings:
```
Added: HKCU\Software\Microsoft\Windows\CurrentVersion\Run\Malware
Modified: HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters
```
- Process and Thread Activity: The malware might spawn new processes or inject code into existing ones. Example findings:
```
Created: Process PID 1234 (malicious_process.exe)
Injected: Thread into explorer.exe
```

- Network Activity: In Wireshark, you could observe the malware attempting to communicate with external servers, which may include sending HTTP requests or establishing TCP connections. Example findings:
```
GET http://malicious-domain.com/command
TCP connection to 192.168.1.100:8080
```

By completing this exercise, you will gain practical experience in dynamic malware analysis, allowing you to identify and understand the behavior and impact of malicious software in a controlled and safe environment.







