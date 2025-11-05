<p align="center">
  <img src="https://raw.githubusercontent.com/morshedmilton/OneDrive-fix-for-mod-windows/main/onedrive-logo.png" alt="OneDrive Logo" width="120" height="120">
</p>

<h1 align="center">OneDrive Fix for Mod-Windows</h1>

<p align="center">
  <strong>A simple batch script to fix OneDrive sign-in errors on modified Windows 10 & 11 installations.</strong>
  <br>
  <br>
  <a href="https://github.com/morshedmilton/OneDrive-fix-for-mod-windows/issues">
    <img alt="Issues" src="https://img.shields.io/github/issues/morshedmilton/OneDrive-fix-for-mod-windows?style=for-the-badge&color=5DADE2">
  </a>
  <a href="https://github.com/morshedmilton/OneDrive-fix-for-mod-windows/stargazers">
    <img alt="Stargazers" src="https://img.shields.io/github/stars/morshedmilton/OneDrive-fix-for-mod-windows?style=for-the-badge&color=F1C40F">
  </a>
  <a href="https://github.com/morshedmilton/OneDrive-fix-for-mod-windows/network/members">
    <img alt="Forks" src="https://img.shields.io/github/forks/morshedmilton/OneDrive-fix-for-mod-windows?style=for-the-badge&color=82E0AA">
  </a>
  <a href="https://github.com/morshedmilton/OneDrive-fix-for-mod-windows/LICENSE">
    <img alt="License" src="https://img.shields.io/github/license/morshedmilton/OneDrive-fix-for-mod-windows?style=for-the-badge">
  </a>
</p>

---

## ⚠️ The Problem

Have you installed a lightweight, "modded" or "debloated" version of Windows 10 or 11 (like Ghost Spectre, ReviOS, Nexus LITEOS, etc.) only to find that you can't sign in to OneDrive?

You might see errors like:
* *"You can't sign in here with a personal account. Use your work or school account instead."*
* *"There was a problem signing you in. (Error Code: 0x8004de40)"*
* Or the sign-in window simply closes with no error.

This happens because many custom Windows ISOs remove or modify components and permissions that OneDrive relies on. This script aims to fix that.

---

## 📋 Table of Contents

* [🎯 Supported Systems](#-supported-systems)
* [🚀 How to Use](#-how-to-use)
* [✨ What It Does](#-what-it-does)
* [❗ Disclaimer](#-disclaimer)
* [🤝 Contributing](#-contributing)
* [🙏 Acknowledgments](#-acknowledgments)

---

## 🎯 Supported Systems

This fix is intended for **modified versions of Windows 10 and 11**, including (but not limited to):

* 👻 **Ghost Spectre**
* ⚙️ **ReviOS**
* 💡 **Nexus LITEOS**
* ...and other similar custom, debloated, or "modded" ISOs.

If you are on a standard, official version of Windows, you should try Microsoft's official [OneDrive troubleshooter](https://support.microsoft.com/en-us/office/reset-onedrive-34701e00-bf7b-42db-b960-84905399050c) first.

---

## 🚀 How to Use

No installation is needed. Just download and run the script.

1.  Go to the main page of this repository.
2.  Click the green **`<> Code`** button.
3.  Select **`Download ZIP`**.
4.  Extract the ZIP file to a folder (e.g., your Desktop).
5.  Inside the folder, right-click on `OneDrive-Fix.bat` and select **"Run as administrator"**.
6.  Follow the on-screen prompts in the command window.
7.  Once the script is finished, **restart your computer** and try signing in to OneDrive again.

---

## ✨ What It Does

This batch script runs a series of commands to restore missing components and fix broken permissions.

* **Restores Permissions:** Takes ownership and resets permissions for critical system and app folders that OneDrive needs to access.
* **System File Check:** Runs `sfc /scannow` to find and repair any corrupt or missing system files.
* **DISM RestoreHealth:** Runs `DISM /Online /Cleanup-Image /RestoreHealth` to repair the Windows Component Store.
* **Resets OneDrive:** (Optional) Attempts to reset the OneDrive application itself.

*(Note: You can improve this section by adding more specific details about what `OneDrive-Fix.bat` does!)*

---

## ❗ Disclaimer

**This script is designed for *modified* operating systems that are already in a non-standard state.** It runs powerful system-level commands to modify permissions and repair files.

**USE THIS SCRIPT AT YOUR OWN RISK.**

I am not responsible for any data loss or system instability. It is **highly recommended** to **create a System Restore Point** before running this script.

---

## 🤝 Contributing

Contributions are what make the open-source community such an amazing place! If you have a suggestion, a fix, or an improvement:

1.  Fork the Project
2.  Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3.  Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4.  Push to the Branch (`git push origin feature/AmazingFeature`)
5.  Open a Pull Request

---

## 🙏 Acknowledgments

* (Add any links or users here that helped you find the solution)
* ...
