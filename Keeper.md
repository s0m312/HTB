## Guided:
**Q:** How many open TCP ports are listening on Keeper?<br>
**A:** 2

**Q:** What is the default password for the default user on Request Tracker (RT)?<br>
**A:** password <br>
> `root:password`

**Q:** Besides root, what other user is in RT?<br>
**A:** lnorgaard

**Q:** What is the lnorgaard user's password on Keeper?<br>
**A:** Welcome2023!

**Q:** Submit the flag located in the lnorgaard user's home directory.<br>
**A:** 8c63c9dc0be85b6282ecfff9b6fde6de

**Q:** What is the 2023 CVE ID for a vulnerability in KeePass that allows an attacker access to the database's master password from a memory dump?<br>
**A:** CVE-2023-32784

**Q:** What is the master password for passcodes.kdbx?<br>
**A:** rødgrød med fløde<br>
> had to google they password (Ippsec hint), the dump showed me `dgrd med flde` or "●Mdgr●d med fl●de" <br> but thats because i dont have Denish language at computer.

**Q:** What is the first line of the "Notes" section for the entry in the database containing a private SSH key?<br>
**A:** PuTTY-User-Key-File-3: ssh-rsa <br>
> use `kpcli` or `keepassxc` 

**A:** Submit the flag located in the root user's home directory. <br>
**Q:** de14b50e0f249c3ac9ffd4cd2055aeac<br>
> Used PuTTy to login, like this:<br>
> Launch PuTTY but do not connect to a remote system.<br>
> In the Category window, browse to Connection>Data.<br>
> Set the Auto-login username to the remote SSH username. ...<br>
> Browse to Connection>SSH>Auth>Credentials. ...<br>
> Test key-based authentication. ...<br>
> Select Open to test the session.
