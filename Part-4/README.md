# Windows Server 2022: **Setting Up a Windows 11 VM and Joining It to a Domain**

## Prerequisites

- VirtualBox installed
- Windows 11 Pro or Enterprise ISO (Home edition will **not** work,  domain join requires Pro/Enterprise)
- An existing Windows Server VM with Active Directory Domain Services (AD DS) installed and configured
- A domain already created
- Administrator credentials for the domain controller

## **Part 1: Creating the Windows 11 VM**

1. Open **VirtualBox**.
2. Click **New** to create a brand new machine.
3. Name the machine (e.g., `Windows 11 Labs`).
4. Select the Windows 11 ISO and proceed through the setup wizard.
5. Click **Finish**.
6. Start the VM.

<img width="702" height="554" alt="image" src="https://github.com/user-attachments/assets/9bf379e1-1cb5-4f56-a897-0749869c9222" />

> **Note:** Windows 11 installation can be difficult to bypass without a Microsoft account. Disconnecting the network during installation can help avoid the login/account creation screens, though registry keys may still be required in some cases.
> 

## Part 2: Windows 11 Installation

1. Boot the VM from the Windows 11 ISO.
2. Accept the terms of agreement.
3. **Important:** Select **Windows 11 Pro** or **Enterprise** during installation 
4. Complete the installation. If prompted to create an account, you may create a local user or use registry workarounds to bypass the Microsoft account requirement.

## Part 3: Configuring the Windows 11 VM Network Settings

<img width="665" height="519" alt="image 1" src="https://github.com/user-attachments/assets/9a3333a8-a232-4a87-813a-e555f7b388bf" />

1. In VirtualBox, open the VM's **Settings** → **Network**.
2. Set **Adapter 1** to **Host-only Adapter** (this isolates the VM from the internet for lab purposes).

<img width="394" height="213" alt="image 2" src="https://github.com/user-attachments/assets/a301c3a7-e279-45c3-858f-ef08104830a3" />

1. Enable the adapter and apply changes.

<img width="380" height="241" alt="image 3" src="https://github.com/user-attachments/assets/b9e03851-6626-4d57-89b4-5c448c07f8db" />

1. Inside Windows 11, open **Network Settings** → **Change adapter options**.
2. Right-click the adapter → **Properties** → **Internet Protocol Version 4 (TCP/IPv4)**.
3. Configure the IP address:
    - **IP address:** `10.1.10.3`
    - **Subnet mask:** `255.255.255.0`
    - **Default gateway:** `10.1.10.1`
    
    <img width="379" height="437" alt="image 4" src="https://github.com/user-attachments/assets/bcdcaf5b-312f-48f2-94fa-8d5e7c1adac0" />
    
4. Click **OK** to save.

> The domain controller is configured at `10.1.10.2` (or `10.1.10.1` depending on setup) on the same subnet.
> 

## Part 4: Renaming the PC (Optional but Recommended)

<img width="588" height="284" alt="image 5" src="https://github.com/user-attachments/assets/0f409364-1b57-4f42-afd4-aa4bccd69e90" />

1. Right-click **This PC** → **Properties**.
2. Click **Rename this PC**.
3. Enter a new name
4. Restart the VM when prompted.

---

## Part 5: Joining the Domain

1. Verify connectivity by opening **Command Prompt** and pinging the domain controller:
    
    text
    
    ```
    ping 10.1.10.2
    ```
    
2. Right-click **This PC** → **Properties**.
3. Under **Computer name, domain, and workgroup settings**, click **Change**.
4. Select **Domain** and enter the domain name.
5. When prompted, enter the **domain administrator credentials**.
6. If successful, a welcome message confirms the domain join.
7. Restart the VM

## Part 6: Logging In with a Domain Account

1. At the Windows login screen, select **Other user**.
2. Enter the domain username  and password.
3. You should now be logged into the domain-joined Windows 11 machine.

> You can now test domain user accounts and verify that domain policies apply.
> 

---

## Part 7: Remote Desktop Connection (Optional)

<img width="349" height="400" alt="image 6" src="https://github.com/user-attachments/assets/b3af29ef-c754-4a0a-a770-7c0545d0a916" />

1. On the Windows 11 VM, right-click **This PC** → **Properties** → **Remote settings**.
2. Enable **Allow remote connections to this computer**.
3. Add users who are allowed to connect (Administrator already has access by default).
4. From another machine, open **Remote Desktop Connection** and enter the IP address of the Windows 11 VM to connect.
