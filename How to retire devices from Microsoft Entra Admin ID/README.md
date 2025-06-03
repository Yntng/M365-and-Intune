# 🔧 How to Retire Devices from Microsoft Entra ID

This guide explains how to retire or delete stale, unused, or decommissioned devices from Microsoft Entra ID (formerly Azure AD).

---

## 📌 Prerequisites

- **Global Administrator**, **Cloud Device Administrator**, or **Intune Administrator** role.
- Access to [Microsoft Entra Admin Center](https://portal.azure.com/).
- Optional: Access to **Microsoft Intune Admin Center** if managing via Intune.

---

## ✅ Step-by-Step: Retire Devices via Entra Admin Center

1. Go to [https://portal.azure.com](https://portal.azure.com)

![Alt text](images/Azure%20url.png)

2. Select Microsoft Entra ID:

![Alt text](images/MS%20Entra%20ID.png)

3. In left-hand menu, select the **Devices** section, you will see an overview of all devices enrolled in Microsoft Entra ID.

![Alt text](images/Overview.png)

4. Locate and **select the list of devices** that have been successfully rolled out.

![Alt text](images/Devices%20rolled.png)

5. Use the **search bar** at the top to find the specific device by name.

![Alt text](images/Search%20devices.png)

6. Once the device appears in the results, **select the device**.

![Alt text](images/Select%20device%20to%20retire.png)

7. Click on the **"Manage"** option at the top of the page.

8. In the management toolbar, click on the **"Retire"** button.

![Alt text](images/retire.png)

9. Confirm the action to **retire the device** from Microsoft Entra.

> ℹ️ Retiring a device removes it from active management but does not factory reset it. For a full wipe, consider using the **Wipe** option from Microsoft Intune if applicable.
