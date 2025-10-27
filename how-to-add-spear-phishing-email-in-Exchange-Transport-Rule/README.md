

## Manual Blocking of Spear Phishing Emails in Microsoft 365 Admin Center

### Step 1: Sign in to Microsoft 365 Admin Center
- Navigate to https://admin.microsoft.com.
- Log in using your **Global Administrator** or **Security Administrator**credentials.


![Alt text](images/Admin%20Center.png)
---

### Step 2: Access Exchange Admin Center (EAC)
- In the left-hand navigation pane, go to:
  **Admin centers > Exchange**
- This will open the **Exchange Admin Center** in a new browser tab.

![Alt text](images/Exchange.png)
---

### Step 3: Create a Mail Flow Rule to Block Sender/Domain
1. In the Exchange Admin Center, go to:
   **Mail Flow > Rules**

![Alt text](images/Mail%20flow.png)

2. Click **+ Add a rule** > **Create a new rule**.

![Alt text](images/Rules.png)

3. Enter a name for the rule (e.g., `Block Spear Phishing Sender`).

![Alt text](images/Edit.png)

4. Under **Apply this rule if**:
   - Select **The sender is** and add the suspicious email address or domain.

![Alt text](images/Condition%20Rules.png)


5. Under **Do the following**:
   - Choose **Delete the message without notifying anyone** or **Quarantine the message**.


![Alt text](images/Add%20block%20list%20email.png)

6. Click **Save**, review the settings, and then click **Save** to activate the rule.