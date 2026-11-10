# Incident Handler's Journal

> **Instructions:** Use this template to record findings after completing an activity, take notes on specific tools or concepts, or log key takeaways from the cybersecurity course.

---

## Entry 001

| Field           | Details                      |
|-----------------|------------------------------|
| **Date**        | 3 November 2026              |
| **Description** | Ransomware security incident |
| **Tools Used**  | SIEM, Host IDS               |

### The 5 W’s

* **Who:** A group of unethical hackers.
* **What:** Attackers gained access to the company’s network using malware. The software was installed on employee computers, and the files were encrypted, preventing employees from accessing their work.
* **When:** Tuesday, 3 November 2026 (data was encrypted on this date).
* **Why:** Phishing emails were sent with a malicious attachment. Employees installed the malware on their computers, granting attackers access to the company’s network.

### Additional Notes / Open Questions

To be investigated:

1. Why were the phishing emails not filtered by the email gateway?
2. Why did employees not raise a phishing alert?
3. Why did employees open the attached file?
4. Why was the malware not detected by the host-based security software?

---

## Entry 002

| Field           | Details                                                  |
|-----------------|----------------------------------------------------------|
| **Date**        | 7 November 2026                                          |
| **Description** | Suspicious file hash                                     |
| **Tools Used**  | [VirusTotal](https://www.virustotal.com/gui/home/search) |

### The 5 W’s

* **Who:** Unknown threat actor (linked to DarkHotel-related campaigns).
* **What:** An alert was triggered about a suspicious file being downloaded on an employee’s computer. Multiple unauthorized executable files were created after the file was opened.
* **When:** Saturday, 7 November 2026, 1:20 p.m.
* **Where:** On an employee’s workstation.
* **Why:** An employee received an email with a file attachment, downloaded it, and opened it — triggering the malware execution chain.

### Additional Notes

The suspicious file was analyzed via VirusTotal → **Verdict: Malicious**.

> “The analyzed binary is a backdoor and credential-stealing trojan, historically associated with DarkHotel-related campaigns. It utilizes Internet Explorer COM automation to scrape C2 instructions and payloads from `http://org.misecure.com/index.html`, steals stored credentials via `CredEnumerateA` and `CryptUnprotectData` (specifically targeting `Microsoft_WinInet_` web credentials), executes shell commands using redirected pipes (`CreatePipe`, `CreateProcessW`), downloads and executes secondary payloads via `ShellExecuteA`, exfiltrates stolen data via HTTP query parameters (`d?flag=` and `d?flagpro=`), and automatically suppresses security prompts using `FindWindowW` and `PostMessageW`.”

**IoCs extracted:**
- C2 URL: `http://org.misecure.com/index.html`
- Exfil params: `d?flag=`, `d?flagpro=`
- API calls: `CredEnumerateA`, `CryptUnprotectData`, `CreatePipe`, `CreateProcessW`, `ShellExecuteA`, `FindWindowW`, `PostMessageW`

---

## Entry 003

| Field           | Details                                                                       |
|-----------------|-------------------------------------------------------------------------------|
| **Date**        | 8 November 2026                                                               |
| **Description** | Phishing alert investigation                                                  |
| **Tools Used**  | Ticketing system <br>[VirusTotal](https://www.virustotal.com/gui/home/search) |

### The 5 W’s

* **Who:** Employee which received pshishing email.
* **What:** Phishing alert was received.
* **When:** Sunday, 8 November 2026, 1:20 p.m.
* **Where:** Employees computer.
* **Why:** Employee opened downloaded attachment from phising email.

### Additional Notes

Ticket with alerted email details
Malicious sender
Subject with grammar errors
File is executable
File Hash was investigated using VirusTotal tool – marked as malicious.
--- 
## Entry 004

| Field           | Details                         |
|-----------------|---------------------------------|
| **Date**        | 7 November 2026                 |
| **Description** | Capturing packets using tcpdump |
| **Tools Used**  | Tcpdump                         |


### Actions
Task 1. Identify network interfaces: 
<br>
`sudo tcpdump -D` 
<br>
Task 2. Inspect the network traffic of a network interface with tcpdump
<br>
`sudo tcpdump -i eth0 -v -c5`
<br>
Task 3. Capture network traffic with tcpdump
<br>
`sudo tcpdump -i eth0 -nn -c9 port 80 -w capture.pcap &`
<br>
Task 4. Filter the captured packet data
<br>
`sudo tcpdump -nn -r capture.pcap -v`

### Additional notes

Tcpdump is very useful cybersecurity tools for packet analysis that captures and displays network traffic in real-time.

---
## Entry 005

| Field           | Details                                   |
|-----------------|-------------------------------------------|
| **Date**        | 7 November 2026                           |
| **Description** | Explore signatures and logs with Suricata |
| **Tools Used**  | Suricata                                  |


### Actions

Task 1. Examine a custom rule in Suricata
`cat custom.rules`
<br>
Task 2. Trigger a custom rule in Suricata
`sudo suricata -r sample.pcap -S custom.rules -k none`
<br>
`cat /var/log/suricata/fast.log`
<br>
`cat /var/log/suricata/eve.json`
<br>
`jq ./var/log/suricata/eve.json | less`
<br>
`jq -c "[.timestamp,.flow_id,.alert.signature,.proto,.dest_ip]" /var/log/suricata/eve.json`
<br>
`jq "select(.flow_id==X)" /var/log/suricata/eve.json`
<br>

### Additional notes

Suricata is very useful cybersecirty tool for network analysis and threat detection.

