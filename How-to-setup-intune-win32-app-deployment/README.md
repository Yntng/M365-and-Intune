# Deploying a Win32 App via Intune Company Portal

Guide for packaging a downloaded `.exe` and publishing it to Company Portal on Intune-enrolled (Entra ID joined) devices.

## 1. Prerequisites

- The app installer (`.exe` or `.msi`)
- Its silent/unattended install switch (check vendor docs, or run `setup.exe /?` or `/help`)
- [Microsoft Win32 Content Prep Tool](https://github.com/microsoft/Microsoft-Win32-Content-Prep-Tool) (`IntuneWinAppUtil.exe`)
- Intune admin center access: https://intune.microsoft.com

## 2. Package the .exe into .intunewin

1. Put the installer alone in its own source folder (no other unrelated files).
2. Download `IntuneWinAppUtil.exe` and run it from the folder you saved it to:

   ```
   cd C:\Users\<yourname>\Downloads
   IntuneWinAppUtil.exe
   ```

3. Answer the interactive prompts in order:
   - **Source folder**: full path to the folder containing the installer
     (e.g. `C:\Users\<yourname>\Downloads\MyApp`)
   - **Setup file**: just the filename (e.g. `setup.exe`), not the full path
   - **Output folder**: where to save the resulting `.intunewin` file

## 3. Create the app in Intune

Go to **Apps > All apps > Add**, choose **Windows app (Win32)**, upload the `.intunewin` file, then fill in each tab below.

### App information

| Field | Notes |
|---|---|
| Name | User-facing name shown in Company Portal |
| Description | Short summary of what the app does |
| Publisher | Vendor name |
| App Version | Version string, if known |
| Category | Existing or new category (e.g. "Productivity") |
| Show as featured app | Optional |
| Information URL / Privacy URL | Optional |
| Logo | Upload a `.png` icon |

### Program

| Field | Example |
|---|---|
| Install command | `setup.exe /VERYSILENT /SUPPRESSMSGBOXES /NORESTART` |
| Uninstall command | `"C:\Program Files\<AppName>\unins000.exe" /VERYSILENT /SUPPRESSMSGBOXES /NORESTART` |
| Install behavior | System (recommended) or User |
| Device restart behavior | "Determine behavior based on return codes" (default) |

**Common silent install switches by installer type:**

| Installer framework | Silent switch |
|---|---|
| Inno Setup | `/VERYSILENT /SUPPRESSMSGBOXES /NORESTART` |
| InstallShield | `/s /v"/qn"` (sometimes `/silent` or `/s`) |
| NSIS | `/S` |
| MSI / WiX bootstrapper | `/quiet` or `/qn` |
| Squirrel (common for Electron apps) | Often no silent install — not a great Intune candidate |

Uninstall commands are trickier since the original `.exe` isn't present post-install — locate the actual uninstaller path via a test install (commonly under `C:\Program Files\<AppName>\` or the registry's `UninstallString`).

### Requirements

- **OS architecture**: 32-bit / 64-bit (usually both)
- **Minimum OS version**: e.g. Windows 10 1607+
- **Disk space / memory / logical processors**: optional, only if the app has real minimums
- **Additional requirement rules**: optional (e.g. require a specific registry key or file to already exist)

### Detection rules

Use **Manually configure detection rules** for a plain `.exe`. Pick one rule type:

- **MSI product code** — if the exe wraps an MSI (find via `Get-WmiObject Win32_Product` or vendor docs)
- **File exists** — e.g. `C:\Program Files\<AppName>\<AppName>.exe`, optionally matching a version number
- **Registry key exists** — e.g. `HKLM\SOFTWARE\<Publisher>\<AppName>` checking a version value

Prefer a version-matched File or Registry rule over a bare "exists" check — more reliable for detecting updates.

### Dependencies

- Leave empty for a standalone app.
- If the app requires a prerequisite (e.g. .NET Runtime, Visual C++ Redistributable) already in Intune: **Add dependency** → select it → mark **Automatically install**.

### Supersedence

- Leave empty for a first-time deployment.
- Use later when uploading a newer version, to have it replace/uninstall the older one automatically.

### Scope tags

- Leave default unless your org uses scope tags for delegated admin visibility.

### Assignments

| Assignment type | Purpose |
|---|---|
| Required | Force-installs on target devices/users automatically |
| **Available for enrolled devices** | Shows in Company Portal for self-service install — use this to make it "available" |
| Uninstall | Force-removes from target devices/users |

### Review + create

- Check every tab for warning indicators before submitting.
- Click **Create**.
- Monitor rollout under **Apps > Monitor > App install status**.

## 4. Verify

On a test enrolled device:

1. Open **Company Portal**, sync, and confirm the app appears under **Apps**.
2. Cross-check install status in Intune under **Apps > Monitor > App install status**.
