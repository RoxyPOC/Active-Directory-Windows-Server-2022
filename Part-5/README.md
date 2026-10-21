# Windows Server 2022: R**eplicating Help Desk IT Issues - Account Management & Group Policy**

## Scenario 1: Disabling a User Account (Employee Offboarding)

<img width="164" height="274" alt="image" src="https://github.com/user-attachments/assets/a13a7165-2513-412e-8017-6825069c3af2" />

1. On the domain controller, open **Active Directory Users and Computers** (via **Tools**).
2. Locate the user
3. Right-click the account → **Disable Account**.
4. A downward arrow on the account icon indicates the account is disabled.
5. Restart the Windows 11 client machine.

---

## Scenario 2: Replicating the Disabled Account Issue (Clearing Cached Credentials)

**Problem:** Windows caches credentials and user profiles locally, so a disabled account may still appear to log in on a machine where the profile already exists.

### Steps to replicate the issue properly:

<img width="509" height="407" alt="image 1" src="https://github.com/user-attachments/assets/40135018-e865-42b5-b0f8-383d03c020cd" />

1. Sign out of the current session.
2. Log in using a **local administrator account** 
3. Right-click **This PC** → **Properties** → **Advanced system settings** → **User Profiles** → **Settings**.
4. Select User’s profile→ **Delete** (removes the cached profile completely).
5. Sign out.
6. Attempt to sign back in as the user.

> **Result:** Login now fails — the disabled account can no longer authenticate.
> 

---

## Scenario 3: Configuring Logon Hours

<img width="441" height="282" alt="image 2" src="https://github.com/user-attachments/assets/f90a065c-5c7b-4ef0-8371-d2ef11935226" />

1. In **Active Directory Users and Computers**, right-click the user → **Properties** → **Account** tab.
2. Click **Logon Hours**.
3. Set **all hours to "Logon Denied"** (100% off).
4. Click **Apply** → **OK**.
5. Attempt to log in as the user.

<img width="547" height="179" alt="image 3" src="https://github.com/user-attachments/assets/4b48197b-0939-4dd0-8e5b-681f7d6e1ea0" />

> **Result:** Error message: *"The account has time restrictions that prevent you from signing in at this time. Please try again later."*
> 

---

## Scenario 4: Account Expiration

1. In the user's **Account** tab, under **Account expires**, select **End of** and set a date (or **Never** to remove expiration).
2. Attempt to log in after the expiration date.

<img width="339" height="123" alt="image 4" src="https://github.com/user-attachments/assets/4b81c7ef-c4a5-4e2b-85d4-40933a628603" />

> **Result:** Error message: *"The user account has expired."*
> 

---

## Scenario 5: Configuring Group Policy (Password & Lockout Policies)

### Accessing Group Policy

<img width="652" height="460" alt="image 5" src="https://github.com/user-attachments/assets/cf8637f9-4254-4608-91ab-1c5adcc455f1" />

1. On the domain controller, open **Tools** → **Group Policy Management**.
2. Navigate to **Forest** → **Domains** → **your domain** → **Default Domain Policy**.
3. Right-click → **Edit**.

### Password Policy

<img width="687" height="504" alt="image 6" src="https://github.com/user-attachments/assets/73864717-0403-4b92-91dc-5a538764e0cc" />

Navigate to: **Computer Configuration** → **Policies** → **Windows Settings** → **Security Settings** → **Account Policies** → **Password Policy**

| Setting | Value Used | Notes |
| --- | --- | --- |
| Maximum password age | **90 days** | Common ranges: 30–120 days depending on environment |
| Minimum password age | **1 day** | Prevents immediate password cycling |
| Minimum password length | **12+ characters** | Recommended for audits  |

### Account Lockout Policy

<img width="677" height="486" alt="image 7" src="https://github.com/user-attachments/assets/52e10cf3-ac19-4b27-b131-fd1ecdc8a423" />

Navigate to: **Account Policies** → **Account Lockout Policy**

| Setting | Value Used | Notes |
| --- | --- | --- |
| Account lockout threshold | **3 invalid attempts** | Number of failed logins before lockout |
| Account lockout duration | **360 minutes** | Longer duration helps prevent brute-force attacks (30 min is common, but 360 min is stricter) |

### Enforcing the Policy

1. Right-click the policy → **Enforced**.
2. On the client machine, open **Command Prompt** and run:
    
    ```
    gpupdate /force
    ```
    
    or
    
    ```
    gpresult /r
    ```
    
    to view applied policies.
    

### Verifying Password Policy

Run on the client:

```
net user user /domain
```

Output shows:

- Password last set
- Password expires (e.g., 90 days from set date)

---

## Scenario 6: Testing Account Lockout

1. Attempt to log in as user with an incorrect password **3 times**.
2. The account becomes locked out.

### Unlocking the Account

1. In **Active Directory Users and Computers**, locate the user.
2. Double-click the account → **Account** tab.
3. Check **Unlock account**.
4. Click **Apply** → **OK**.
5. The user can now log in again.

---

## Scenario 7: Resetting a User Password

1. In **Active Directory Users and Computers**, right-click the user → **Reset Password**.
2. Enter a new password.
3. (Optional) Require password change at next logon.
4. Apply and confirm.
