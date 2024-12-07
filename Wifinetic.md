## Guided:
**Q:** What is the name of the OpenWRT backup file accessible over FTP?<br>
**A:** backup-OpenWrt-2023-07-26.tar<br>
> ftp allows anonymous login

**Q:** Whats the WiFi password for SSID OpenWRT?<br>
**A:** VeRyUniUqWiFIPasswrd1!<br>
> /etc/wireless file contains the password for user `netadmin`

**Q:** Which user reused the WiFi password on thier local account?<br>
**A:** netadmin <br>
> /etc/passwd file contains the username

**Q:** Submit the flag located in the netadmin user's home directory.<br>
**A:** eab560a054002b7d4e9d02a2259d7ea6

**Q:** What user space daemon software is being used to create access point and authentication servers?<br>
**A:** hostapd<br>
> `ps aux`, at the end of the list i could see it

**Q:** Which interface is being used for monitoring?<br>
**A:** mon0
> `iwconfig` reveals it |or| `iw dev` |or| `ip link show` 

**Q:** What is the WPA password for the network on the mon0 interface?<br>
**A:** WhatIsRealAnDWhAtIsNot51121!
> As mentioned at the pdf file inside the tar file i found on ftp,<br> they installed reaver
> `reaver -i mon0 -b <MAC> -c 1` |or|<br> `reaver -i <monitor-interface> -b <target-MAC> -c <channel`

**Q:** Submit the flag located on the root folder.<br>
**A:** a759ae69e3eb05388a613d88f8a3a144
