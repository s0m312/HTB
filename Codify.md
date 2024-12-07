## Guided:
**Q:** Which is the highest open TCP port on Codify?<br>
**A:** 3000 <br>
> `nmap -F <IP>`

**Q:** What is the relative path on the web application that offers a form to run JavaScript code?<br>
**A:** /editor

**Q:** What is the name of the sandboxing library used by the application?<br>
**A:** vm2
> (revealed at "contact us")

**Q:** What is the 2023 CVE ID assigned to a remote code execution vulnerability in vm2 that was patched in version 3.9.17?<br>
**A:** CVE-2023-30547
this [link](https://gist.github.com/leesh3288/381b230b04936dd4d74aaf90cc8bb244) helped me upload reverse-shell 

**Q:** What user is the web application running as?<br>
**A:** svc

**Q:** There is a second NodeJS application on Codify that isn't running. What is the name of the SQLite database file used by this application?<br>
**A:** tickets.db<br>
> found in /var/www/

**Q:** What is the joshua user's password on Codify?<br>
**A:** spongebob1

**Q:** Submit the flag located in the joshua user's home directory.<br>
**A:** d6b49eff8e6f66a4f8a510b574381820

**Q:** What is the full path of the script that the joshua user can run as root?<br>
**A:** /opt/scripts/mysql-backup.sh

**Q:** Which single character is accepeted as the password, bypassing the password check in the script?<br>
**A:** *

**Q:** What is the root user's MySQL password?<br>
**A:** kljh12k3jhaskjh12kjh3<br>
> uploaded `pspy64` and used it with svc user while using the `mysql-backup.sh`

**Q:** Submit the flag located in the root user's home directory.<br>
**A:** 17e3fc8411678d8d782677d7c08f16ed
