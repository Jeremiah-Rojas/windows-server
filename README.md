# Windows Server 2019 Vulnerability Remediation
In this lab I created a Windows Server 2019 Vm on Azure and installed purposely outdated software; I was curious to see what Nessus would tell me to do to remediate these because the easiest way to remove the vulnerabilities is to just uninstall the apps. 
</br>
### Here is some of the insecure software I installed:
- Python 2.7.18
- WinRAR 5.50
</br>
</br>Note: Python can serve as a tool for automation, system management, development, data analysis, and security testing.
</br>Note: WinRAR is a file archiver and compression utility on Windows, widely used to compress, extract, and manage archive files.

</br>I then ran a credentialed Nessus scan against the machine and found the following:
