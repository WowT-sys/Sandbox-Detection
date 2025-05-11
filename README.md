# Sandbox Detection

## Overview
This is a C program designed to detect whether it is running inside a **sandboxed** or **virtualized environment**. It uses differences in CPU instruction execution timing to determine if the environment is virtualized, which is a common technique for detecting sandboxes or virtual machines.

---

## How It Works
The program runs two parallel tasks:
1. A thread repeatedly executes the `FYL2XP1` x87 FPU instruction (a logarithmic operation).
2. The main thread executes the `CPUID` instruction in a loop.

By measuring the ratio of how many times the `FYL2XP1` instruction executes relative to the number of `CPUID` instructions, the program determines whether it is running in a sandbox. Virtualized environments often introduce overhead for certain instructions, which can skew this ratio.

If the ratio exceeds a predefined threshold, the program concludes that it is running in a sandbox.

---

## Features
- Detects sandboxed or virtualized environments.
- Calculates a confidence score for sandbox detection.
- Uses low-level CPU instructions (`FYL2XP1` and `CPUID`) for detection.

---

## Requirements
- **Operating System**: Windows
- **Compiler**: A C compiler that supports inline assembly (e.g., MinGW or MSVC)
- **Privileges**: Administrator privileges may be required to run the program in some environments.

---

## Usage
1. Clone the repository or download the source code.
2. Compile the program using a C compiler. For example:
   ```bash
   gcc -o sandbox-detect sandbox-detect.c
   ```
3. Run the program:
   ```bash
   ./sandbox-detect
   ```

---

## Output
The program will output:
1. The number of `FYL2XP1` executions (`c`).
2. The ratio of `FYL2XP1` executions to `CPUID` executions.
3. A message if a sandbox is detected.
4. A confidence score indicating the likelihood of being in a sandbox.

Example output:
```
c=500000, ratio=5.000000
SANDBOX DETECTED!!!
95.000000% confident sandbox
```
---

## Customization
You can modify the following constants in the code:
- `THRESHOLD`: The ratio threshold for detecting a sandbox. Default is `5.0`.
- `ITERATIONS`: The number of `CPUID` instructions to execute. Default is `1000000`.

---

## Warning
This program is for educational and research purposes only. It is designed to demonstrate sandbox detection techniques and should not be used for malicious purposes. Use responsibly and in compliance with applicable laws.

---
## Disclaimer
The detection method used in this program is not foolproof and may produce false positives or negatives depending on the environment. It is intended as a demonstration of sandbox detection techniques, not as a definitive detection tool.
---
