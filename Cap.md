## Guided:
**Q:** How many TCP ports are open?<br>
**A:** 3 <br>
`nmap -p- -sV -Pn -T4 <IP>`(honestly it showed me 7)<br>

**Q:** After running a "Security Snapshot", the browser is redirected to a path of the format /[something]/[id], where [id] represents the id number of the scan. What is the [something]?<br>
**A:** data<br>
> Once I've visited the site, Opened the dash board (on the left)<br> Security Snapshot (5 Second Pcap + analysis) ,<br> there was an `Download` Option on the bottom,<br> but inspecting it, it revealed an Event that let to `http://<IP>/data/1`<br>

**Q:** Are you able to get to other users' scans?<br>
**A:** Yes<br>
> By inspecting the pages threw debugger on the browser,<br> I've looked for "href" it led to `http://<IP>/download/1` ,<br> so i tryed 2,3 but it didnt let me go over 2,<br> so i tryed 0 and it worked.

**Q:** What is the ID of the PCAP file that contains sensative data?<br>
**A:** 0

**Q:** Which application layer protocol in the pcap file can the sensetive data be found in?
**A:** ftp<br>
Opened the Pcap file in wireshark and saw credentials in clear text for user `nathan:Buck3tH4TF0RM3!`<br>

**Q:** We've managed to collect nathan's FTP password.<br> On what other service does this password work?<br>
**A:** ssh<br>
> Always cred spray on other services once user's creds have been found.

**Q:** Submit the flag located in the nathan user's home directory.<br>
**A:** c279868e982851f7c8cb4dc9e324dee9

**Q:** What is the full path to the binary on this machine has special capabilities that can be abused to obtain root privileges?<br>
**A:** /usr/bin/python3.8<br>
> linpeas helped me. even tho.. this would do the job `getcap -r / 2>/dev/null`<br>
> Pivot was to type down this:
>            `/usr/bin/python3.8 -c 'import os; os.setuid(0); os.system("/bin/bash")`

**Q:** Submit the flag located in root's home directory.<br>
**A:** d33c379ceef1370ccedc51cf6d83bfd7
