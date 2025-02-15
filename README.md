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

## **✅ Conclusion**
- **Brute force attack executed & detected** in Windows logs.
- **Logs successfully uploaded & analyzed in Splunk Cloud.**

🚀 Lab completed!

