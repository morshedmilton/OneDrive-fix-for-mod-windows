# OneDrive Fix Guide for Modded Windows

> Easily restore OneDrive functionality on custom or "debloated" Windows 10/11 builds.  
> **This guide walks you through each fix in clear steps.**

***

## 🚩 Overview

Many custom Windows ISOs (Ghost Spectre, ReviOS, Nexus LITEOS, etc.) block or break OneDrive due to altered system policies or removed components.

**This guide helps you:**
- Restore registry permissions
- Enable essential Windows services
- Add OneDrive to startup
- Run optional system repairs

***

## 📝 Step-by-Step Fix

### 1. Fix Registry Block

- Open **Registry Editor** as Administrator.
- Go to:
  ```
  HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\OneDrive
  ```
- Find `DisableFileSyncNGSC` and **change its value** from `1` to `0`.

***

### 2. Enable Required Services

Open **Command Prompt** as Administrator and run:

```
REG ADD "HKLM\System\CurrentControlSet\Services\OneSyncSvc" /v Start /t REG_DWORD /d 3 /f
REG ADD "HKLM\System\CurrentControlSet\Services\UserDataSvc" /v Start /t REG_DWORD /d 3 /f
REG ADD "HKLM\System\CurrentControlSet\Services\UnistoreSvc" /v Start /t REG_DWORD /d 3 /f
REG ADD "HKLM\System\CurrentControlSet\Services\PimIndexMaintenanceSvc" /v Start /t REG_DWORD /d 3 /f
```
***

### 3. Set UserServiceFlags

In the same Command Prompt, run:

```
REG ADD "HKLM\System\CurrentControlSet\Services\OneSyncSvc" /v UserServiceFlags /t REG_DWORD /d 3 /f
REG ADD "HKLM\System\CurrentControlSet\Services\UserDataSvc" /v UserServiceFlags /t REG_DWORD /d 3 /f
REG ADD "HKLM\System\CurrentControlSet\Services\UnistoreSvc" /v UserServiceFlags /t REG_DWORD /d 3 /f
REG ADD "HKLM\System\CurrentControlSet\Services\PimIndexMaintenanceSvc" /v UserServiceFlags /t REG_DWORD /d 3 /f
```
***

### 4. Add OneDrive to Startup

Still in Command Prompt, enter:
```
REG ADD "HKCU\Software\Microsoft\Windows\CurrentVersion\Run" /v OneDrive /t REG_SZ /d "%LOCALAPPDATA%\Microsoft\OneDrive\OneDrive.exe /background" /f
```

***

### 5. Restart Your PC

**Restart your computer** to apply all changes.

***

### 6. Launch OneDrive

After reboot, run manually:
```
"%LOCALAPPDATA%\Microsoft\OneDrive\OneDrive.exe"
```

***

### 🛠️ Optional: System Repair (if OneDrive still fails)

If OneDrive still won't start, try:
```
sfc /scannow
DISM /Online /Cleanup-Image /RestoreHealth
```
> *Restart your computer again and test OneDrive.*

***

## ⚠️ Disclaimer

- These fixes modify Windows system settings.
- **Backup your data** and consider creating a Restore Point.
- Use at your own risk.

***

## 💡 Tips

- For official Windows, consider the [OneDrive Troubleshooter](https://support.microsoft.com/en-us/office/reset-onedrive-34701e00-bf7b-42db-b960-84905399050c).
- Still problems? Ask for help or check for updates!

***

## 🤝 Contribute!

Spotted a bug? Got improvements? PRs are welcome! Help make these guides better for everyone.

***
