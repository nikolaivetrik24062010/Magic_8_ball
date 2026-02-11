# Magic 8 Ball – Logic Deconstruction & Reverse Engineering Case Study

A lightweight Android application designed as a **Security Research Sandbox**. This project is specifically architected to demonstrate the vulnerabilities of **Hardcoded Business Logic** and the risks associated with **Client-Side Predictability**. It serves as an entry-level project for practicing static and dynamic analysis.

---

## 🎯 Security Research Objectives

The core purpose of this project is to explore how an attacker can manipulate "Black Box" logic when it is hosted entirely on the device.

* **Logic Extraction:** Practicing the recovery of original source code from a compiled APK using `Jadx`.
* **Predictability Analysis:** Analyzing the entropy of client-side random number generators (RNG) and how they can be seeded or predicted.
* **Runtime Manipulation:** Using **Frida** to hook the "answer engine" and force a specific outcome (e.g., always returning "Yes").
* **Binary Hardening:** Comparing the "Readability" of the code before and after applying **R8/ProGuard** obfuscation.



---

## 🔍 Attack Surface: Predictability & Trust

Even in a simple app, critical AppSec principles are at play:

- **Insecure Randomness:** Researching why `java.util.Random` is insufficient for secure applications and how it can be bypassed.
- **Hardcoded Strings:** Analyzing the leakage of sensitive or proprietary strings within the compiled binary.
- **Tampering Vulnerability:** Demonstrating how an attacker can modify the `.dex` file and re-sign the APK to change the application's behavior.
- **Logic Exposure:** Understanding that any business rule (e.g., a "Win/Loss" decision) implemented strictly in Kotlin is visible to anyone with access to the APK.



---

## 🛡️ Defensive Research & Hardening

### 1. Anti-Tampering & Obfuscation
- **R8 Integration:** Implementation of strict obfuscation rules to mangle method names and strip debug metadata, increasing the time and cost of reverse engineering.
- **Resource Protection:** Analyzing how string obfuscation can prevent simple `grep` attacks on the binary.

### 2. Architectural Security
- **Moving the "Source of Truth":** Discussion on why critical logic should be moved to a trusted execution environment (TEE) or a remote backend for high-stakes applications.
- **Integrity Verification:** (Planned) Exploring the use of the **Play Integrity API** to ensure the app hasn't been modified or re-signed.

---

## 🧠 Technical Stack
- **Language:** Kotlin
- **UI:** XML-based simple view interaction
- **Security Tools:** Jadx-GUI (Static), Frida (Dynamic), MobSF (Vulnerability Scanning).

---

## 🧪 AppSec Practice Scenarios
- **Scenario A:** Use Jadx to find the array of answers and modify them.
- **Scenario B:** Write a Frida script to intercept the `Random.nextInt()` call and return a constant value.
- **Scenario C:** Analyze the app with MobSF to identify common manifest misconfigurations.

---

## 👤 Author
**Nikolay Vetrik** – *Senior Security Engineer & Mobile Developer* 📧 [devnikolaivetrik@gmail.com](mailto:devnikolaivetrik@gmail.com) | 🔗 [LinkedIn](https://www.linkedin.com/in/nikolayvetrik24062010/)

---

## ⚠️ Disclaimer
This project is intended **strictly for educational research and defensive security analysis**. It focuses on the fundamental risks of client-side logic and the necessity of application hardening.
