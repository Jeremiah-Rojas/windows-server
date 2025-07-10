# Windows Server 2019 Vulnerability Remediation
In this lab I created a Windows Server 2019 Vm on Azure and installed purposely outdated software; I was curious to see what Nessus would tell me to do to remediate these because the easiest way to remove the vulnerabilities is to just uninstall the apps. 
</br>
### Here is some of the insecure software I installed:
- Python 2.7.18
- WinRAR 5.50

</br>Note: Python can serve as a tool for automation, system management, development, data analysis, and security testing.
</br>Note: WinRAR is a file archiver and compression utility on Windows, widely used to compress, extract, and manage archive files.

</br>I then ran a credentialed Nessus scan against the machine and found the following:
<img width="1522" height="667" alt="image" src="https://github.com/user-attachments/assets/9569fa5f-0dbb-4d1b-bf0b-5bddc2b54aec" />

</br>After looking at the “Remediations” tab, I was very surprised to find only two actions that needed to be taken:
<img width="1175" height="151" alt="image" src="https://github.com/user-attachments/assets/d4bd5249-567a-49c2-8473-6a593a45e65d" />

## Remediations

For the WinRAR update, I navigated to this website https://www.win-rar.com/download.html, and simply installed the more up-to-date version. By doing so, it overrides the previous version.
<img width="1719" height="727" alt="image" src="https://github.com/user-attachments/assets/c01c35e0-260d-4570-8f59-e0a69c11af49" />

The other remediation is to install something called “KB5062557”; this is a windows update and is fixed by updating the system.
<img width="1456" height="636" alt="image" src="https://github.com/user-attachments/assets/176032a5-8d3e-4692-9686-78fbd888fe56" />

After this, I ran another scan and found a noticable reduction in vulnerabilities:
<img width="1518" height="524" alt="image" src="https://github.com/user-attachments/assets/4f7acedd-7716-4500-a571-3c2a7a208b8d" />

### Remaining Vulnerabilities (and fixes):
- High: Add and enable registry value EnableCertPaddingCheck.
-       Add this registry value: HKEY_LOCAL_MACHINE\Software\Microsoft\Cryptography\Wintrust\Config\EnableCertPaddingCheck
- Medium: SMB signing not required.
-       In Group Policy Editor, Navigate here; Computer Configuration > Windows Settings > Security Settings > Local Policies > Security Options. Then enable “Microsoft network client: Digitally sign communications (always)” and “Microsoft network server: Digitally sign communications (always).”
- Medium: TLS Version 1.0/1.1 Protocol Detection. Enable support for TLS 1.2 and 1.3, and disable support for TLS 1.0/1.1.
-       Add the following keys:
      HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client
      HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server
      Then enter the appropriate DWORD values
- Low: ICMP Timestamp Request Remote Date Disclosure.
-       Open Group Policy Editor and navigate to: Computer Configuration > Windows Settings > Security Settings > Windows Defender Firewall with Advanced Security
-   Create a new inbound rule: 
-     Type: Custom
-     Protocol: ICMPv4
-     ICMP Settings: Specific ICMP types → Timestamp Request (Type 13)
-     Action: Block
-     Profile: All
-     Name: Block ICMP Timestamp Request

