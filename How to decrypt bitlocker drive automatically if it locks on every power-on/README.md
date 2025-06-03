# 1. BitLocker on Reboot Error

## 🔍 Check TPM Status

1. Open **PowerShell** in **Administrator mode**.
2. Run the following command:

    ```powershell
    get-tpm
    ```

3. Check the TPM status:

    - `TpmPresent: True`  
    - `TpmReady: True`  
    - `TpmEnabled: True`

---

## ⚠️ If TPM is `False`

If any of the TPM values return `False`, follow these steps:

### ✅ Enable TPM in BIOS/UEFI

1. **Restart your computer** and enter the **BIOS/UEFI settings**:
    - Common keys: `Del`, `F2`, `F10`, or `Esc` (varies by manufacturer).
2. Go to the **Security** or **Advanced** tab.
3. Locate and **enable TPM** (may be listed as **TPM**, **PTT** for Intel, or **fTPM** for AMD).
4. Save and exit BIOS.
5. Boot into Windows and re-run:

    ```powershell
    get-tpm
    ```

6. Confirm:
    - `TpmPresent: True`  
    - `TpmReady: True`  
    - `TpmEnabled: True`

---

## 🔓 Ensure Drives Are Decrypted Before Enabling BitLocker

Before enabling BitLocker, make sure **all drives are decrypted**:

1. Open **PowerShell** as Administrator.
2. Run this command to check the encryption status of all drives:

    ```powershell
    Get-BitLockerVolume
    ```

3. If any drives show `EncryptionMethod` as not `None`, decrypt them:

    ```powershell
    Disable-BitLocker -MountPoint "D:"
    ```

> 🔁 Repeat the `Disable-BitLocker` command for each encrypted drive.

---

## 🛠 Enable Auto-Unlock After Verifying TPM & Decryption

Once TPM is enabled and all drives are decrypted, you can enable BitLocker Auto-Unlock for fixed drives:

```powershell
Enable-BitLockerAutoUnlock -MountPoint "D:"
