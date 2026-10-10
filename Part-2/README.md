# **Windows Server 2022: Rename the Server and Install Active Directory**

## Goal

Rename the Windows Server VM and promote it to a domain controller for a new Active Directory forest.

## 1. Rename the server

1. Sign in to the server using the Administrator account.
2. Open **Server Manager → Local Server**.
3. Select the current computer name, then choose **Change**.

<img width="587" height="410" alt="image" src="https://github.com/user-attachments/assets/4eb60877-fa23-4dfa-ab2b-019f1f11074d" />

1. Enter a descriptive name, such as `MY-DC-01`.

<img width="356" height="413" alt="image 1" src="https://github.com/user-attachments/assets/c93b3bbf-4fdd-4267-9105-03360793b6d0" />

1. Apply the change and restart the server.
2. Sign in again after the restart.

## 2. Install the Active Directory Domain Services role

1. In Server Manager, select **Manage → Add Roles and Features**.

<img width="318" height="161" alt="image 2" src="https://github.com/user-attachments/assets/2835a37d-ff29-4eab-be5d-89f4b3dd28fc" />

1. Continue through the wizard to **Server Roles**.
2. Select **Active Directory Domain Services (AD DS)**.

<img width="678" height="490" alt="image 3" src="https://github.com/user-attachments/assets/e47bff2d-3f0b-4236-ad4c-df4bb53addee" />

1. Choose **Add Features** when prompted to include required components.
2. Continue through the remaining pages, leaving defaults unless your lab requires otherwise.
3. Select **Install** and wait for the role installation to complete.

Installing the role does not yet create a domain controller. The server must still be promoted.

## 3. Promote the server to a domain controller

1. In Server Manager, select the notifications flag.
2. Choose **Promote this server to a domain controller**.
3. Select **Add a new forest**, since this lab has no existing domain.

<img width="658" height="488" alt="image 4" src="https://github.com/user-attachments/assets/029b4613-7a9b-476f-b2a0-a0d80cd9e643" />

1. Enter a root domain name.
    - Use a domain name you control or a clearly designated lab name. Avoid using a real organization’s domain without authorization.
2. Set the forest and domain functional levels as appropriate for the lab. Prefer the newest level supported by your environment rather than lowering it unnecessarily.
3. Set and securely record the Directory Services Restore Mode (DSRM) password.

<img width="660" height="474" alt="image 5" src="https://github.com/user-attachments/assets/c32af88b-3679-4a89-8335-ffe0c74b6941" />

1. Continue through the wizard. Review the DNS, NetBIOS, and paths pages; defaults are usually suitable for a basic lab.
2. Review the prerequisite checks, then select **Install**.
3. Allow the server to restart. Promotion can take several minutes, depending on the VM’s resources.

## Optional: PowerShell installation

The promotion wizard can generate a PowerShell command for the selected configuration. An administrator can run the reviewed command in an elevated PowerShell session instead of completing the promotion through the GUI. 

## 4. Verify the installation

After the restart, sign in with a domain account, then check the server and domain configuration.

Useful commands include:

cmd

```
whoami
systeminfo
```

- `whoami` displays the current account and domain context.
- `systeminfo` displays operating-system and system details, including the computer name and domain information.

You can also open **Active Directory Users and Computers** from Server Manager’s **Tools** menu to confirm that the domain is available.

## 5. DNS Installation

We can uncheck “Create DNS delegation” then click “Next” then “Install”.

<img width="620" height="502" alt="image 6" src="https://github.com/user-attachments/assets/84e21793-6118-4d57-a061-b81b31033377" />

<img width="658" height="546" alt="image 7" src="https://github.com/user-attachments/assets/6a791e96-1059-4ddc-9078-0bda862d2076" />

1. After this process, the virtual machine will restart to install Active Directory Domain Services. Once the restart is complete, sign back in by selecting "Input" and clicking the "Ctrl + Alt + Del" button. You will notice that the domain controller is now listed. Go ahead and sign in to your account using the domain credentials.
2. Once signed in, with Server Manager open, click on "Tools" in the top right corner, then select "Active Directory Users and Computers" from the dropdown menu.
