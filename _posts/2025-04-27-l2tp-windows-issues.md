---
layout: post
title:  "L2TP/IPSec Issues within Windows 10/11"
date:   2025-04-27
tags:   windows win11 vpn support
---

I've been experiencing persistent issues establishing a functional L2TP/IPSec VPN connection at home. After thorough research, I discovered that modifying the Windows registry was necessary to enable proper operation.

1. **Open Command Prompt as Administrator**:
- Press `Win + X` and select `Windows Terminal (Admin)` or `Command Prompt (Admin)`.
1. **Add Registry Entries**:
- Copy and paste the following commands into the Command Prompt and press `Enter` after each command:

**PowerShell**
```
REG ADD HKLM\SYSTEM\CurrentControlSet\Services\PolicyAgent /v AssumeUDPEncapsulationContextOnSendRule /t REG_DWORD /d 0x2 /f
REG ADD HKLM\SYSTEM\CurrentControlSet\Services\RasMan\Parameters /v ProhibitIpSec /t REG_DWORD /d 0x0 /f
```

3. **Restart Your Computer**:
    - After executing the commands, restart your computer to apply the changes.

### Explanation

1. **AssumeUDPEncapsulationContextOnSendRule**:
- This registry entry allows IPSec to work in a NAT (Network Address Translation) environment. Setting it to `0x2` enables IPSec to traverse NAT, which is essential for many home and small office networks.
1. **ProhibitIpSec**:
- This registry entry ensures that IPSec is not prohibited, allowing L2TP/IPSec VPN to function correctly.