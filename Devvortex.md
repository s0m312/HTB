## Guided:
**Q:** How many open TCP ports are listening on Devvortex?<br>
**A:** 2 <br>
> `Nmap -F -sV -sC <IP>`

**Q:** What subdomain is configured on the target's web server?<br>
**A:** dev.devvortex.htb<br>
> `gobuster vhost -w <wordlist> -u <http://something.htb> --append-domain`<br>
> Note: must add this to /etc/hosts to continue.<br>
**Q:** What Content Management System (CMS) is running on dev.devvortex.htb?<br>
**A:** Joomla<br>
> `feroxbuster --url "http://devvortex.htb" --wordlist /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt --threads 100 --extensions "php,txt,js,xml,md,html" --random-agent --filter-status 404,502,504` <br>
> by enum hidden paths, found this: `http://dev.devvortex.htb/README.txt`

**Q:** Which version of Joomla is running on the target system?<br>
**A:** 4.2.6

**Q:** What is the 2023 CVE ID for an information disclosure vulnerability in the version of Joomla running on DevVortex?<br>
**A:** CVE-2023-23752<br>
> msfconsole named it "joomla_api_improper_access_checks"

**Q:** What is the lewis user's password for the CMS?<br>
**A:** P4ntherg0t1n5r3c0n## <br>
> Had to login into the CMS, edit one of the pages to serve as reverse-shell, found here : [Pentest-Monkey](https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php) <br>
> Once i was in, i used lewis creds to login the mysql and pull the hashes.

**Q:** What table in the database contains hashed credentials for the logan user?<br>
**A:** sd4fg_users

**Q:** What is the logan user's password on DevVortex?<br>
**A:** tequieromucho<br>
> `john --show=formats passes` -> `hashcat --help | grep "bcrypt"` -> mode 3200
`$2y$10$IT4k5kmSGvHSO9d6M/1w0eYiB5Ne9XzArQRFJTGThNiy/yBtkIj12:tequieromucho`

**Q:** Submit the flag located in the logan user's home directory.<br>
**A:** 98808b26d1fbaa097a3f3552eca60aa0

**Q:** What is the full path to the binary that the lewis user can run with root privileges using sudo?<br>
**A:** /usr/bin/apport-cli

**Q:** What is the 2023 CVE ID of the privilege escalation vulnerability in the installed version of apport-cli?<br>
**A:** CVE-2023-1326 <br>
> Note: at first, /var/crashes is empty,<br> so i had to create one with flag -f ,<br> once the system showed me `:` at the end, i just had to press `!/bin/bash` <br>
> Understood it thanks to : [CVE-2023-1326](https://github.com/NyxByt3/CVE-2023-1326)

**Q:** Submit the flag located in the root user's home directory.<br>
**A:** b2233530a94f343880da4a6897f4d960
