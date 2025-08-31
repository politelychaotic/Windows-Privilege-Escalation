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

These may be in the format like:

    <Credentials>
        <Username>Administrator</Username>
        <Domain>thm.local</Domain>
        <Password>MyPassword123</Password>
    </Credentials>


### Powershell History

Anytime a user runs a command using Powershell, it is stored in a file. This helps with repeating commands, but if a user runs a command that includes a password directly in the command, it can later be retrieved by using this command in cmd:

    type %userprofile%\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt

That command only works for cmd, to run from Powershell replace `%userprofile` with `$Env:userprofile`



### Saved Windows Credentials

Windows let's you use the credentials of other users. This also allows us to save credentials to the system. This command will list saved credentials:
    
    cmdkey /list

While you can't see the actual passwords, if you notice any credentials worth trying, you can use them with the `runas` command and the `/savecred` option:

    runas /savecred /user:admin cmd.exe

### IIS Configuration (Internet Information Services)

The IIS is the default web server on Windows. The config for websites on IIS is stored in `web.config`, which can store passwords for databased or configured authentication mechanisms. 
Depending on the version, `web.config` can be found in one of these locations:
    1. `C:\inetpub\wwwroot\web.config`
    2. `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\web.config`

A quick method to find connection stringson the file:

    type C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\web.config | findstr connectionString

### Retrieve Credentials from PuTTY

PuTTY is an SSH client found commonly on Windows machines. Users can store sessions which includes IP, user, and other configurations. 
PuTTY does NOT allow users to store SSH passwords, but they can store proxy configurations that store cleartext credentials.

To retrieve the stored proxy credentials, you can search under the following registry key for ProxyPassword with the following command:

    reg query HKEY_CURRENT_USER\Software\SimonTatham\PuTTY\Sessions\ /f "Proxy" /s

*_Note: Simon Tatham is the creator of PuTTY (and his name is part of the path), not the username for which we are retrieving the password. The stored proxy username should also be visible after running the command above._*


Just as putty stores credentials, any software that stores passwords, including browsers, email clients, FTP clients, SSH clients, VNC software and others, will have methods to recover any passwords the user has saved.
