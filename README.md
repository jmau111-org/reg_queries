#  Windows Reg

Cheat sheet reg queries Windows

TO BE CONTINUED indefinitely...

![GitHub last commit](https://img.shields.io/github/last-commit/jmau111-org/windows_reg?label=last%20update%3A)

## Read information

### Get user env var

```
reg query HKCU\Environment /v {Variable Name}
```

### Get AppData path

```
reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders /v AppData
```

### Get user document's folder

```
reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\Shell Folders
```

### Get last registred key

```
reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Applets\RegEdit /v LastKey
```

### Get typed URL

```
reg query HKCU\Software\Microsoft\InternetExplorer\TypedURLS
```

### Inspect autologon

```powershell
reg query "HKLM\SOFTWARE\Microsoft\Windows NT\Currentversion\Winlogon" 2>nul | findstr "DefaultUserName DefaultDomainName DefaultPassword"
```

### Inspect startup

```powershell
reg query HKLM\Software\Microsoft\Windows\CurrentVersion\RunOnce
reg query HKCU\Software\Microsoft\Windows\CurrentVersion\RunOnce
reg query HKLM\Software\Microsoft\Windows\CurrentVersion\Run
reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Run
```

### Get system policies

```
reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System
```

### Get security policy

```
reg query HKLM\SYSTEM\CurrentControlSet\Control\Lsa /v forceguest
```

### Get automatic updates status

```
reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update /v AUOptions
```

### Get Admin token

```
reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v FilterAdministratorToken
```

### Get Windows Defender settings 

=> Group Policy switch:

```
reg query HKLM\SOFTWARE\Policies\Microsoft\Windows Defender /v DisableAntiSpyware
```

### Get service config

```
reg query HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services /s
```

### Get Firewall config

```
reg query HKLM\SYSTEM\CurrentControlSet\Services\SharedAccess\Parameters\FirewallPolicy
```

### Get UAC (User Account Control) config

```
reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v ConsentPromptBehaviorAdmin
```

### Get autorun config

```
reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\Explorer /v NoDriveTypeAutoRun
```

### Wrapper to search terms

=> Get all keys that match "XXX":

```
reg query HKLM\SOFTWARE\Microsoft /s /f XXX /k
```

## Tweak settings

### ⚠️ Take cover

🚨 **Always backup** the Registry **before** tweaking entries! 🚨

### Windows Defender

#### Disable Windows Defender

```
reg add "HKLM\SOFTWARE\Policies\Microsoft\Windows Defender" /v DisableAntiSpyware /t REG_DWORD /d 1 /f
```

#### Enable Windows Defender

```
reg delete "HKLM\SOFTWARE\Policies\Microsoft\Windows Defender" /v DisableAntiSpyware
```

### UAC

#### Disable UAC

```
reg add "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System" /v EnableLUA /t REG_DWORD /d 0 /f
```

#### Enable UAC

```
reg add "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System" /v EnableLUA /t REG_DWORD /d 1 /f
```

## Useful links

* [Windows Commands: reg](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/reg)
