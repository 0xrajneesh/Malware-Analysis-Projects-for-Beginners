# Project 1: Static Analysis of a Simple Malware Sample

## Introduction
Static analysis is the process of analyzing malware without executing it. This method involves examining the file's code and structure to gain insights into its functionality and behavior. In this project, you will perform static analysis on a simple malware sample using various tools to extract information such as strings, PE headers, imports/exports, and embedded resources.

## Pre-requisites
- Basic understanding of malware and its types.
- Familiarity with Windows operating system internals.
- Knowledge of programming languages like C/C++ (optional but helpful).
- Familiarity with common malware analysis tools.

## Lab Set-up
- Operating System: A Windows virtual machine (VM) is recommended. You can use VirtualBox or VMware to create a VM.
- Malware Sample: Obtain a known and safe-to-analyze malware sample from a reputable source like MalwareBazaar.

## Tools:
- PEview: For examining PE headers.
- Strings: For extracting strings from the binary.
- Dependency Walker: For analyzing imports and exports.
- Resource Hacker: For viewing embedded resources.
- Hex Editor (HxD): For examining the binary at a low level.
- Ensure that your VM is isolated from your main network to prevent accidental infection.

## Exercises
### Exercise 1: Extracting Strings

Objective: Extract and analyze strings from the malware sample to gather initial clues about its functionality.


Step 1: Use Strings.exe from Sysinternals.
Step 2: Run Command
```shell
strings malware_sample.exe > strings_output.txt
```
Step 3: Analysis
Open strings_output.txt.
Look for URLs, IP addresses, file paths, registry keys, and other readable text.
Identify any suspicious or noteworthy strings.

Step 4: Retreive the output
After running the strings command, you might find URLs that could indicate command-and-control servers or file paths showing where the malware operates. 

Example findings:
```
Copy code
http://malicious-site.com
C:\Windows\System32\malicious.dll
HKEY_LOCAL_MACHINE\Software\Malware
```

### Exercise 2: Analyzing the PE Header

Objective: Examine the PE header to understand the structure and metadata of the malware sample.


Step 1: Open the malware sample in PEview.
Step 2: Analysis
- Review the sections (e.g., .text, .data, .rdata).
- Note the entry point, which is where the execution starts.
- Check the timestamp to see when the file was compiled.

Step 3: Retreive the output
In PEview, you might observe the following:
- sections
  ```
  kotlin
  Copy code
  .text (code section)
  .data (initialized data)
  .rdata (read-only data)
  ```
- Entry Point: Located in the .text section.
- Timestamp: Indicates the compile date, which can be compared with known malware activity timelines.

### Exercise 3: Inspecting Imports and Exports

Objective: Identify functions that the malware imports from system libraries and any exported functions.



Step 1: Use Dependency Walker.
Step 2: Analysis
- Load the malware sample in Dependency Walker.
- Examine imported functions and their corresponding libraries.
- Check for any exported functions.

Step 3: Solution
You might find the malware imports functions related to networking (e.g., WSAStartup, connect) and file operations (e.g., CreateFile, WriteFile). This indicates potential capabilities like network communication and file manipulation.

Exercise 4: Viewing Embedded Resources

Objective: Examine any resources embedded within the malware sample.



Step 1: Open the malware sample in Resource Hacker.
Step 2: Analysis
Browse through different resource types (e.g., icons, dialogs, strings).
Identify any suspicious or unusual resources.
Step 3: Solution
In Resource Hacker, you may find:

- Icons: Custom icons used by the malware.
- Dialogs: Fake error messages or GUI components.
- Strings: Hardcoded messages or paths.

### Exercise 5: Hex Analysis

Objective: Perform a low-level examination of the binary to uncover any hidden data or patterns.


Step 1:Open the malware sample in HxD (or any hex editor).
Step 2: Analysis
Browse through the binary data.
Look for any readable text or unusual patterns.
Step 3: Solution
In HxD, you might see obfuscated strings or encrypted data. Recognizable patterns could indicate embedded code or data structures.

By completing these exercises, you'll gain a solid foundation in static malware analysis, enabling you to extract valuable information without executing potentially harmful code.
