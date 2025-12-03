# Windows-Process-Injector-C
Shellcode Injection using WinAPI. Educational research on memory manipulation and EDR evasion techniques.
# Windows Process Injector PoC (WinAPI)

![Language](https://img.shields.io/badge/Language-C-blue)
![Platform](https://img.shields.io/badge/Platform-Windows-0078D6?logo=windows)
![Category](https://img.shields.io/badge/Category-Malware%20Analysis-red)

## 🦠 Overview
This repository contains a C implementation of the **Classic Code Injection** technique. It demonstrates how malware interacts with the Windows OS to hide malicious code inside legitimate processes (e.g., `notepad.exe`).

Writing this injector is a fundamental exercise for **Malware Analysts** to understand the specific WinAPI calls used by threat actors, making it easier to identify them during Reverse Engineering and behavioral analysis.

## 🛠️ Technical Details

The injection process follows the standard 4-step pattern used by many malware families:

1.  **OpenProcess:** Acquires a handle to the target process using the PID.
2.  **VirtualAllocEx:** Allocates memory within the target process's address space.
3.  **WriteProcessMemory:** Writes the shellcode (payload) into the allocated memory.
4.  **CreateRemoteThread:** Creates a new thread in the target process to execute the payload.
   
💻 Compilation
To compile this project, use MinGW or Visual Studio Command Prompt:

Bash: gcc injector.c -o injector.exe

🚀 Usage
Open a dummy process (e.g., Notepad).

Find its PID (via Task Manager or tasklist).

Run the injector:

Bash: injector.exe PID

⚠️ Legal Disclaimer
FOR EDUCATIONAL AND RESEARCH PURPOSES ONLY.

This code is provided to help security professionals understand memory injection techniques to improve detection capabilities (EDR testing).

Do not use against systems you do not own.

The author assumes no liability for misuse.

Project developed as part of the Advanced Cybersecurity Portfolio.

```mermaid
graph TD
    A[Injector.exe] -->|1. Open Handle| B(Target Process / PID)
    A -->|2. Allocate Memory| B
    A -->|3. Copy Shellcode| B
    A -->|4. Start Thread| B
    B -->|Executes| C[Malicious Payload]
