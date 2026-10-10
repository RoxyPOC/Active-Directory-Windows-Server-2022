# Windows Server 2022: \VirtualBox Shared Folders and Active Directory Users

## Goal

Install VirtualBox Guest Additions, configure a shared folder for transferring files, and practice creating and managing Active Directory user accounts.

## 1. Install VirtualBox Guest Additions

1. Start the Windows Server 2022 VM and sign in.
2. In the VirtualBox window, select **Devices → Insert Guest Additions CD Image**.

<img width="479" height="359" alt="image" src="https://github.com/user-attachments/assets/61d24f9f-7bff-4322-9ff3-81b39adbdf1c" />

1. In the VM, open the mounted CD drive and run the Guest Additions installer.
2. Follow the prompts and restart the VM if requested.

Guest Additions improves integration between the host computer and the virtual machine, including shared-folder support.

## 2. Create and configure a shared folder

1. On the host computer, create a folder for the lab, such as `HelpDeskLab`.
2. In VirtualBox, open the VM’s **Settings → Shared Folders**.

<img width="332" height="190" alt="image 1" src="https://github.com/user-attachments/assets/bd9e6d72-01a3-45ee-b5cd-49b8be47019b" />

1. Add the host folder and select **Auto-mount** and **Make Permanent**.

<img width="357" height="198" alt="image 2" src="https://github.com/user-attachments/assets/6c57b725-300c-4d66-a446-55c143e66abe" />

1. Start or return to the VM and confirm that the shared folder is accessible.
2. Copy a test file into the shared folder and verify it appears on the other side.

Shared-folder locations can vary depending on the guest OS and VirtualBox configuration. If the folder does not appear, check that Guest Additions installed successfully and that the VM is configured to share the correct host folder.

## 3. Create an Active Directory user

1. Open **Active Directory Users and Computers** from Server Manager’s **Tools** menu.

<img width="738" height="515" alt="image 3" src="https://github.com/user-attachments/assets/3b8bbb77-f6d1-40bd-bf66-2d1a96030941" />

1. Expand the domain and select the appropriate organizational unit, such as **Users**.
2. Right-click the location and choose **New → User**.

<img width="672" height="557" alt="image 4" src="https://github.com/user-attachments/assets/44e28b03-6665-4194-8411-af1847d157d4" />

1. Enter the user’s name and logon name.
2. Set an initial password and configure the password options according to the lab requirements.
3. Select **Next**, then **Finish**.
4. Confirm that the new account appears in the selected container.

Use fictional names and test credentials in a lab. Do not include real people’s personal information or reuse real passwords.

## 4. Manage the user account

In Active Directory Users and Computers, right-click the account or open its **Properties** to practice common help desk tasks:

- **Reset Password** — assign a temporary password. Follow your organization’s identity-verification and password-reset procedures.
- **Disable Account / Enable Account** — block or restore sign-in access.
- **Unlock Account** — unlock an account after it has been locked out.
- **Account properties** — review fields such as department, title, telephone number, and manager. Only enter appropriate, authorized information.
- **Logon Hours** — set permitted logon times when required by policy.
- **Profile** — configure profile-related settings if the environment requires them.

Apply these settings according to organizational policy; avoid restricting logon hours or changing account access without authorization.

## 5. Verify the account

On the domain controller, open Command Prompt and run:

cmd

```
net user josy /domain
```

Replace `josy` with the account’s actual logon name. The command displays domain account details, such as account status, password-related information, and group membership.
