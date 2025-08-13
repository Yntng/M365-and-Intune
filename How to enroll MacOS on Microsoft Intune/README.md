

## 📝 Enrollment Steps

⚠️ *If the Mac had a prior profile, retire it before attempting a data erase.*

###  Download Apple Configurator on your phone

1. Open **Apps Store**  and download  **apple configurator**.
2. Open the Apple Configurator app and proceed through through initial setup. The app must be signed in with a user account from the ASM or ABM account which has been assigned the "Device Enrollment Manager" role. Grant the Bluetooth and camera permissions when prompted, both are required for the enrollment process.

![Alt text](images/Configurator%20app%20.PNG)
![Alt text](images/Configurator%20app%20setup.PNG)

### Step 1: Prepare the Target Mac

1. Power on the **target macOS device**.
2. Proceed through **language selection**.

![Alt text](images/Language%20selection.png)

3. On the **"Country or Region"** selection screen — **STOP** here.

![Alt text](images/Region%20selection.png)

4. The Mac will display a **pairing screen** with a globe.

![Alt text](images/Mac%20scan.png)

5. Scan the **pairing screen** with a app called **Configurator** and let the Mac to process the pairing.


### Step 2: Assign Device to Microsoft Intune in ABM/ASM

1. Go to [business.apple.com](https://business.apple.com).

![Alt text](images/Email%20to%20apple%20business%20manager.png)

2. Sign in and navigate to Devices > Search for your Mac

![Alt text](images/Assign%20Device%20management.png)

3. Select the Mac (it will show as **"Devices Added by Apple Configurator "**).
4. Click ** ... ** **Edit MDM Server**.

![Alt text](images/Choose%20device%20managment.png)

5. Choose the **Intune MDM server** and click **Done**.

![Alt text](images/Device%20management%20service%20assignment%20updated.png)


### Step 3: Assign Enrollment Profile in Intune

1. Go to [Microsoft Intune Admin Center](https://intune.microsoft.com).

![Alt text](images/Admin%20.png)
![Alt text](images/Microsoft%20intune.png)

2. Navigate to Devices > macOS 

![Alt text](images/Intune%20devices.png)
![Alt text](images/Device%20overview.png)

3. Then **Enrollment**

![Alt text](images/Enrollment.png)

4. Then to **Enrollment Program Tokens**

![Alt text](images/Enrollment%20program%20token.png)

5. Select the appropriate **DEP Token**.

![Alt text](images/token%20name.png)

6. Click on **Devices**, then click **Sync** to fetch latest device list.

![Alt text](images/Token%20devices%20and%20sync.png)

7. Locate the target Mac.

![Alt text](images/Select%20device%20and%20assign%20profile.png)

8. Click **Assign profile**.

9. Choose the existing **macOS enrollment profile**.

![Alt text](images/Assign%20profile%20.png)

10. Click **Apply** or **OK**.

---

### Step 5: Complete Setup on the Target Mac

1. Continue the setup process on the target Mac:
- Choose country/region
- Connect to Wi-Fi
2. Click **“Enroll”** to proceed:
> "*[Your Organization] will automatically configure this Mac*"
3. Click **Continue**.
4. Authenticate using your **Microsoft 365 account** credentials.
5. The Mac will **automatically enroll into Intune** and apply all assigned policies and profiles.

---

