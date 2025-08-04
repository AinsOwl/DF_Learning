# 1) Digital Forensics (DF) Concepts

## 🧩 DF Lifecycle – The 5 Critical Steps

1. **Identification**: Determine the specific information that needs to be obtained.
2. **Preservation**: Prevent tampering with the original evidence. Create a forensic copy and conduct all analysis on the copy.
3. **Analysis**: Perform both automated and manual analysis on the copy to confirm or refute a hypothesis regarding the incident.
4. **Documentation**: Record every detail: what evidence was collected, how it was acquired and analyzed, which tools were used, by whom, and how preservation was ensured. This is a **crucial** step.
5. **Presentation**: Deliver the investigation results in a clear, professional report to the requesting party.

---

## 🕵️ DF Investigation Steps

1. **Evidence Acquisition**: Perform forensic imaging using a **write blocker** to create a bit-by-bit copy of the original evidence.
2. **Verification**: Generate **hash signatures** for both the original evidence and its image to ensure integrity. Creating multiple backup copies is advisable.
3. **Preservation**: Store the original evidence in a secure environment. Protect it from humidity, tampering, high temperatures, or any condition that may alter its state.
4. **Analysis**: Extract relevant artifacts to answer key questions: **Who, When, What, Where, How, and Why?**
5. **Validation**: Ensure findings are valid and repeatable. Re-verify with hash checks and re-run analysis to ensure **reproducibility**.

---

## 🧪 Types of Digital Evidence

### 🟠 Volatile Evidence
- Lost once the device is powered off.
- Examples: Data in RAM, cache, routing tables.

### 🟢 Non-Volatile Evidence
- Persists after shutdown.
- Examples: HDDs, SSDs, USB drives, CDs/DVDs.

### User-Created Evidence
- Text files, bookmarks, databases, images, videos, sound files.

### System-Created Evidence
- Activity logs, configuration files, metadata, registry hives, swap files.

---

## 💻 Common Digital Devices

- **HDDs** – Mechanical drives using magnetic storage.
- **SSDs** – Flash-memory drives with no moving parts.
- **RAID** – Combines multiple drives for redundancy and performance.
- **Removable Media** – USBs, memory cards, external drives.
- **RAM** – Volatile memory used for active processes.
- **Mobile Devices** – iOS, Android, Windows phones/tablets.
- **IoT Devices** – Embedded smart devices with network capabilities.
- **Cloud Storage** – Remote data storage via services like AWS, Azure, Google Cloud, etc.

---

## 📜 Chain of Custody (CoC)

A legal document tracking:

- **Who** handled the evidence  
- **Where** it was stored  
- **What** was done to it  
- **Which tools** were used  

> Any missing or inaccurate info in the Chain of Custody may render the evidence **inadmissible in court**.

---

## Setting up Virtual Machine

- Activating Win 10 VM trial > Open CMD as Administrator > slmgr /ato
- If its not your 1st time activating VM > slmgr /rearm
- **Reboot** the VM after running the above command.

---
