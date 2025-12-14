# Endpoint Monitoring with Sysmon and Wazuh
Monitoring devices with sysmon and wazuh. These free tools gives 90% of the skills needed for real SOC EDR workflow.

## Project Overview!!
In this project, I deployed Sysmon on Windows endpoints for deep telemetry, configured Wazuh agents to collect Sysmon event logs, and centralized detection and alerting through the Wazuh manager. This improved visibility into Process creation, PowerShell abuse, and lateral movement, mapped to MITRE ATT&CK




## 📌 Project Overview

This project demonstrates how to build **advanced endpoint monitoring** using **Sysmon**, **Wazuh Agent**, and the **Wazuh Manager**.

It shows how **low-level endpoint telemetry** such as:

- Process creation
- Network connections
- File changes
- Registry modifications

is collected on **Windows endpoints** and centrally analyzed using **Wazuh** for threat detection and security monitoring.

This setup reflects how modern **SOC and Blue Team environments** perform **EDR-like endpoint monitoring** using open-source tools.

---

## 🏗️ Architecture

```text
Windows Endpoint
 ├── Sysmon
 │     └── Generates detailed security events
 │
 ├── Windows Event Log
 │
 └── Wazuh Agent
       └── Collects Sysmon + Windows logs
            ↓
        Wazuh Manager
            ├── Decoders
            ├── Rules
            └── Alerts
            ↓
        Wazuh Dashboard
````

---

## 🔍 Components Explained

### 1️⃣ Sysmon (System Monitor)

**Sysmon** is a Windows system service that provides **deep visibility into endpoint activity**.

It logs:

* Process creation and termination
* Command-line arguments
* Network connections
* File creation and modification
* Registry changes
* DLL loading

All Sysmon events are written to the:

* **Windows Event Log**

---

### 2️⃣ Wazuh Agent

The **Wazuh Agent** is installed on the endpoint and is responsible for:

* Collecting Windows Event Logs
* Forwarding Sysmon logs to the Wazuh Manager
* Performing basic endpoint monitoring (FIM, log collection)

⚠️ **Important:**
The Wazuh Agent does **not replace Sysmon** — it **collects and ships Sysmon telemetry**.

---

### 3️⃣ Wazuh Manager

The **Wazuh Manager** performs centralized security analysis:

* Log decoding
* Rule-based detection
* Alert generation
* Event correlation

It transforms **raw Sysmon logs** into **actionable security alerts**.

---

## ⚖️ Monitoring Comparison

### 🔹 Wazuh Agent Only

Provides:

* Basic endpoint visibility
* Windows Event Logs
* Authentication events
* File Integrity Monitoring (FIM)

**Limitation:**
❌ Limited low-level telemetry
❌ No deep process or network visibility

---

### 🔹 Sysmon + Wazuh (Recommended)

Provides:

* Deep process visibility
* Network connection tracking
* Command-line inspection
* Detection of living-off-the-land (LOLbins) attacks

**Benefit:**
✅ Near **EDR-level monitoring** using open-source tools

---