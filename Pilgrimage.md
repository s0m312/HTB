## Guided:
**Q:** Which version of nginx does the target machine run on TCP port 80?<br>
**A:** 1.18.0

**Q:** What is the name of the directory related to a version-control software that is exposed by the web server?<br>
**A:** .git<br>
> Note: Used git-dumper to extract the .git 

**Q:**  What version of the tool ImageMagick is contained in the web application's repository?<br>
**A:** 7.1.0-49

**Q:** What is the 2022 CVE ID for a file read vulnerability in this version of ImageMagick?<br>
**A:** CVE-2022-44268

**Q:** Where does the web application store its data?<br>
**A:** /var/db/pilgrimage<br>
> Found in `index.php` file that was extracted from .git

**Q:** What is the emily user's password?<br>
**A:** abigchonkyboi123<br>
> Note: Used this -> [CVE-2022-44268](https://github.com/entr0pie/CVE-2022-44268)<br>
> To extract the content off `/var/db/pilgrimage` (also decoded from hex)

**Q:** Submit the flag located in the emily user's home directory.<br>
**A:** daccf6de2693e1a1d485a12f9cadb645

**Q:** What is the full path to the unusual bash script being run by the root user?<br>
**A:** /usr/sbin/malwarescan.sh<br>
> Note: linpeas.sh indicated this + this "ps aux | grep "^root""

**Q:** Which directory is monitored by inotifywait and passes files to binwalk? (Include trailing /).<br>
**A:** /var/www/pilgrimage.htb/shrunk/<br>
> By inspecting this .sh file, this can be seen.

**Q:** What is the 2022 CVE ID for a remote code execution (RCE) vulnerability in this version of binwalk?<br>
**A:** CVE-2022-4510

**Q:** Submit the flag located in the root user's home directory.<br>
**A:** c5ad7f7367416f1b6a16c5237d3af594<br>
> Note: Had to create the .png file with exploit and re-deliver it via the web-site, inorder `/usr/bin/inotifywait` will execute it and i get reverse shell back.
