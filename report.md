# Host & Network Recon Lab - recon01

## Objective
Scan internal lab network to identify active hosts, open ports, running services and potential lateral movement paths. 

## Lab Setup
| Machine       | IP Address     | Role        |
|---------------|----------------|-------------|
| Kali Linux    | 192.168.56.102 | Attacker    |
| Win Server 22 | 192.168.56.101 | Target Host | 

# Nmap Command Used

nmap -sS -sV -O -p- 192.168.56.101 -oN full-scan.txt

# Key Findings
| Port  | State | Service | Notes                     |
|-------|-------|---------|---------------------------|
| 5985  | Open  | wsman   | Windows Remote Management |

- 65,534 ports filtered (no response)
- MAC Address suggests virtual machine (Oracle VirtualBox)
- Latency was minimal: 0.0045s (local network)

# OS Fingerprint
- OS Guess: Microsoft Windows Server 2022/2016 (92% accuracy)
- Other guesses: Windows 11 21H2 (85%), Server 2016 (85%)
- CPEs: cpe:/o:microsoft:windows_server_2022, windows_server_2016, windows_11

# Lateral Movement Considerations
- WinRM (5985) open: could allow remote code execution with valid credentials
- All other ports filtered: likely host-based firewall is enabled
- No open SMB/HTTP/RDP services found at time of scan

# Artifacts
full-scan.txt
report.md
		
