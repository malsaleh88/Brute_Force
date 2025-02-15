# 🚀 Brute Force Attack & Detection with Splunk

## 🔹 **Lab Overview**
In this lab, I performed a **brute force attack** on a Windows machine using **Hydra (Kali Linux)** and detected the attack using **Windows Event Viewer & Splunk Cloud**.

---

## **1️⃣ Brute Force Attack with Hydra**
### **Attack Command:**
```bash
hydra -l administrator -P /usr/share/wordlists/rockyou.txt -t 4 192.168.1.53 ssh
```
- **Target:** Windows VM (`192.168.1.53`)
- **Attack Method:** SSH brute force using `rockyou.txt`
- **Result:** Multiple failed login attempts

![bruto1](https://github.com/user-attachments/assets/742a2433-e827-4760-885d-446ea6991e68)


---

## **2️⃣ Detecting the Attack on Windows**
- Open **Event Viewer (`eventvwr.msc`)**.
- Check **Windows Logs → Security**.
- Found **Event ID 4625** (Failed Logins) from Kali Linux.

---

## **3️⃣ Uploading Logs to Splunk Cloud**
1. **Export Security Logs** from Windows:
   - Save as `brute_force.evtx`
2. **Convert to JSON:**
   ```powershell
   Get-WinEvent -Path "C:\path\to\brute_force.evtx" | ConvertTo-Json -Depth 3 | Out-File "C:\path\to\brute_force.json"
   ```
3. **Upload `brute_force.json` to Splunk Cloud.**

---

## **4️⃣ Searching for Attacks in Splunk Cloud**
- **Detect failed logins:**
  ```spl
  index=main EventCode=4625
  ```

![splaunk1](https://github.com/user-attachments/assets/c345f5c8-1af3-49b2-a58b-90aff55f43cd)



   
---

# 🔍 SSH Security Investigation Report

## Incident Summary
On **February 15, 2025**, multiple failed SSH login attempts were detected on the system. These attempts originated from an unknown source and failed due to incorrect credentials and disabled accounts.

## Key Findings
- **Failed SSH logins detected** (`Event ID: 4625`).
- **Unknown user accounts used** (e.g., `FakeUser`).
- **Logon Type: 3 (Network) & 8 (Explicit Credentials) detected**.
- **Unable to determine source IP** because the attempts originated from **localhost (127.0.0.1)**.

## Conclusion
Since the login attempts came from `localhost`, no external IP address could be identified. Further monitoring and security enhancements have been implemented.

## Next Steps
- Enforce key-based authentication.
- Restrict SSH access to trusted users.
- Monitor security logs for future attempts.

---
📌 *This report documents the investigation and steps taken to improve SSH security.*  

🚀 Lab completed!

