# OneDrive Fix Guide for Modded Windows

> Easily restore OneDrive functionality on custom or "debloated" Windows 10/11 builds (XOS, Ghost Spectre, ReviOS, Nexus LITEOS, etc.).  
> **This comprehensive guide walks you through diagnostic checks and complete fixes.**

***

## 🚩 Overview

Many custom Windows ISOs block or break OneDrive due to altered system policies or removed components. This guide provides a proven solution that has worked successfully for modded Windows installations.

**Common OneDrive Issues:**
- OneDrive sign-in window disappears immediately
- Error: "You can't sign in here with a personal account"
- Error Code: `0x8004de40`
- OneDrive missing from File Explorer
- Services won't start (Error 1077)

***

## 🔍 Quick Diagnostic First

Before applying fixes, run these commands in **Command Prompt as Administrator** to confirm the issues:

### Check Registry Block
```cmd
reg query "HKLM\SOFTWARE\Policies\Microsoft\Windows\OneDrive" /v DisableFileSyncNGSC
```

### Check Service Status
```cmd
sc query "OneSyncSvc"
sc query "UserDataSvc"
sc query "UnistoreSvc"
sc query "PimIndexMaintenanceSvc"
```

### Expected Issues:
- `DisableFileSyncNGSC = 1` (this blocks OneDrive)
- All four services show **STOPPED** with error **1077**

***

## 🛠️ The Complete Fix (Step-by-Step)

### Phase 1: Fix the Registry Block

#### Step 1: Modify Registry

1. Open **Registry Editor** as Administrator
2. Navigate to:
   ```
   HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\OneDrive
   ```
3. Find `DisableFileSyncNGSC`
4. **Change the value** from `1` to `0`
5. Click **OK**

***

### Phase 2: Enable the Service Templates

#### Step 2: Enable Service Startup

Open **Command Prompt as Administrator** and run:

```cmd
REG ADD "HKLM\System\CurrentControlSet\Services\OneSyncSvc" /v Start /t REG_DWORD /d 3 /f
REG ADD "HKLM\System\CurrentControlSet\Services\UserDataSvc" /v Start /t REG_DWORD /d 3 /f
REG ADD "HKLM\System\CurrentControlSet\Services\UnistoreSvc" /v Start /t REG_DWORD /d 3 /f
REG ADD "HKLM\System\CurrentControlSet\Services\PimIndexMaintenanceSvc" /v Start /t REG_DWORD /d 3 /f
```

#### Step 3: Enable Per-User Service Creation

In the same Command Prompt, run:

```cmd
REG ADD "HKLM\System\CurrentControlSet\Services\OneSyncSvc" /v UserServiceFlags /t REG_DWORD /d 3 /f
REG ADD "HKLM\System\CurrentControlSet\Services\UserDataSvc" /v UserServiceFlags /t REG_DWORD /d 3 /f
REG ADD "HKLM\System\CurrentControlSet\Services\UnistoreSvc" /v UserServiceFlags /t REG_DWORD /d 3 /f
REG ADD "HKLM\System\CurrentControlSet\Services\PimIndexMaintenanceSvc" /v UserServiceFlags /t REG_DWORD /d 3 /f
```

#### Step 4: Add OneDrive to Startup

Still in Command Prompt, enter:

```cmd
REG ADD "HKCU\Software\Microsoft\Windows\CurrentVersion\Run" /v OneDrive /t REG_SZ /d "%LOCALAPPDATA%\Microsoft\OneDrive\OneDrive.exe /background" /f
```

***

### Phase 3: Restart and Test

#### Step 5: Restart Your Computer

**⚠️ This step is CRITICAL!** The service template changes only take effect after a full system restart.

- Save all your work
- Restart your computer completely
- Do NOT skip this step

#### Step 6: Launch OneDrive

After restart, try launching OneDrive manually:

```cmd
"%LOCALAPPDATA%\Microsoft\OneDrive\OneDrive.exe"
```

***

## ✅ Expected Results

After completing all steps and restarting, you should see:

- ✅ OneDrive starts without the popup disappearing
- ✅ OneDrive appears in File Explorer navigation pane
- ✅ OneDrive appears in Quick Access
- ✅ OneDrive icon visible in system tray
- ✅ Sign-in works normally

***

## 🔧 If OneDrive Still Doesn't Work

If OneDrive still fails after the restart, run this system repair as Administrator:

```cmd
sfc /scannow
DISM /Online /Cleanup-Image /RestoreHealth
```

> *Wait for both commands to complete (this may take 15-30 minutes), then restart again and test OneDrive.*

***

## ⚠️ Disclaimer

- These fixes modify Windows system settings and registry
- Designed for **modified/debloated Windows installations** (XOS, Ghost Spectre, ReviOS, etc.)
- **Backup your data** and consider creating a System Restore Point before proceeding
- Use at your own risk

***

## 💡 Additional Tips

- **For official Windows:** Consider the [OneDrive Troubleshooter](https://support.microsoft.com/en-us/office/reset-onedrive-34701e00-bf7b-42db-b960-84905399050c)
- **Still having issues?** Make sure all steps were completed in order
- **Services not starting?** Verify you ran commands as Administrator
- **Changes not applying?** Ensure you restarted your computer after Phase 2

***

## 👨‍💻 About This Guide

This solution has been tested and proven successful on:
- XOS Windows 11
- Ghost Spectre Windows 10/11
- ReviOS
- Nexus LITEOS
- Other debloated/modded Windows installations

***

## 🤝 Contribute

Found this helpful? Help others by:
- ⭐ Starring this repository
- 🐛 Reporting issues you encounter
- 💬 Sharing your experience
- 🚀 Contributing improvements via Pull Requests

Spotted a bug? Got improvements? PRs are welcome!

***

## 📝 Summary

1. **Diagnose** - Check registry and services
2. **Fix Registry** - Change `DisableFileSyncNGSC` to 0
3. **Enable Services** - Run registry commands for 4 services
4. **Add Startup** - Register OneDrive in startup
5. **Restart** - MUST restart for changes to apply
6. **Test** - Launch OneDrive manually
7. **Repair (if needed)** - Run SFC and DISM

***

**Good luck! This solution has helped many users successfully restore OneDrive on modded Windows installations.** 🚀
