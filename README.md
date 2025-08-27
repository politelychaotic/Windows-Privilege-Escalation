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

The IIS is the default web server on Windows.
