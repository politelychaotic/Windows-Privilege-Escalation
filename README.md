# Windows-Privilege-Escalation
THM Windows Privilege Escalation Lab



### Unattended Windows Install
Admins sometimes use Windows Deployment Services, which allows for one system image to be deployed to several hosts.
These setups require the admin account for initial setup, which might be stored in the machine in these following locations:
    C:\Unattend.xml
    C:\Windows\Panther\Unattend.xml
    C:\Windows\Panther\Unattend\Unattend.xml
    C:\Windows\system32\sysprep.inf
    C:\Windows\system32\sysprep\sysprep.xml
