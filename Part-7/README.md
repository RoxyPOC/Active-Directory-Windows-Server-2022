## Part 1: Creating a Shared Folder

<img width="610" height="403" alt="image" src="https://github.com/user-attachments/assets/ac249b82-00e4-4940-94e2-967aa5aa1dc7" />

1. On the **server**, open **Server Manager**.
2. Go to **File and Storage Services** → **Shares**.
3. Right-click → **New Share** (or use the shares wizard).
4. Choose the **C: drive**.
5. Name the share
6. On the permissions step, choose **Customize permissions**:
    - **Remove `Everyone`**.
    - Add only **Administrator**.
7. Apply → OK → Next → **Create**.

---

## Part 2: Narrowing Access to a Subfolder

Sharing the whole folder would give users access to everything inside — not desirable. Instead, create a subfolder and share only that.

1. Open the folder
2. Create a new subfolder
3. Right-click the **Tech** folder → **Properties** → **Sharing** → **Advanced Sharing**.

<img width="311" height="415" alt="image 1" src="https://github.com/user-attachments/assets/aff00c6c-0e70-4014-a465-88cc139a7725" />

1. Check **Share this folder**.

<img width="295" height="316" alt="image 2" src="https://github.com/user-attachments/assets/9325f70c-12f8-44cd-a1cf-c235daca175d" />

1. Under **Permissions**, remove `Everyone` (Apply → OK).

<img width="311" height="393" alt="image 3" src="https://github.com/user-attachments/assets/390abca0-23ee-4141-8eb2-a50f55ddbedf" />

### Configure Security (NTFS) Permissions

<img width="307" height="418" alt="image 4" src="https://github.com/user-attachments/assets/5b3715da-aa04-4e06-b89f-449662f6ff4a" />

1. Go to the **Security** tab.
2. Leave **Administrator** 
3. Click **Edit** → **Add** → add the user

<img width="395" height="243" alt="image 5" src="https://github.com/user-attachments/assets/f5ab7208-36c5-4266-baa7-cbaef604597a" />

1. Grant **Modify** (not Full Control).
2. Apply → OK.

### Configure Share Permissions

<img width="527" height="368" alt="image 6" src="https://github.com/user-attachments/assets/d6dfe9c5-6b92-4194-979c-9af0cf5dcbc6" />

1. Under **Sharing** → **Advanced Sharing** → **Permissions**.
2. Add User as **Contributor** with **Read** and **Write** (Change) access.
3. Apply → OK → Share.

---

## Part 3: Verifying Access as the User

1. On the client VM, confirm network/domain connectivity:
    
    ```
    ping server
    ```
    
    (If it fails, check the VM's network adapter,  it must be on the domain network, not host-only.)
    
2. Open **File Explorer** and navigate to:
    
    ```
    \\DC01\Tech
    ```
    
3. Log in as User.

### Expected Results

| Path | Result |
| --- | --- |
| `\\DC01\server`(parent) | **Access denied** , no permissions granted at this level |
| `\\DC01\Tech` (subfolder) | **Access granted** , read/write/modify |

---

## Part 4: Mapping the Share as a Network Drive

<img width="328" height="297" alt="image 7" src="https://github.com/user-attachments/assets/eb15bd4b-b61e-4187-b546-b0dc00e2475c" />

1. In File Explorer, right-click **This PC** → **Show more options** → **Map network drive**.
2. Choose a drive letter (e.g., `Z:`).
3. Paste the UNC path (e.g., `\\DC01\Tech`).
4. Click **Finish**.
5. Verify from Command Prompt:
    
    ```
    net use
    ```
    
    Output confirms the mapping (e.g., `Z:` → `\\DC01\Tech`).
    

> The mapped drive appears in File Explorer; the parent share still cannot be accessed by User.
> 

---

## Part 5: Using Active Directory Security Groups

Instead of granting permissions to individual users, create a **security group** and add users to it.

### Create the Group

<img width="430" height="366" alt="image 8" src="https://github.com/user-attachments/assets/e5c88e74-1f16-44bb-bb03-b3ccc95e89e9" />

1. Open **Active Directory Users and Computers**.
2. Right-click the target OU → **New** → **Group**.
3. Name it (e.g., `Tech`), scope **Global**, type **Security**.

<img width="343" height="391" alt="image 9" src="https://github.com/user-attachments/assets/023dd3ae-5fd8-4b78-880f-ca000db59b2c" />

1. Add User as a member → Apply → OK.

### Assign Folder Permissions to the Group

1. On the `Tech` folder → **Properties** → **Security** → **Edit** → **Add** → add the `Tech` group.
2. Grant **Read** (or Modify, as appropriate).
3. Optionally add a **description** to the group documenting its purpose

### Test Group-Based Access

1. Remove User as a direct permission entry on the folder (leave the group entry).
2. Log in as  User (or restart/sign out and back in to refresh the token).
3. Access `\\DC01\Tech,` it should still work **because User is a member of the `Tech` group**.

---

## Part 6: Inspecting Effective Permissions

1. On the `Tech` folder → **Properties** → **Security** → **Advanced**.
2. Select the user/group → **Effective Access** tab → **Select a user** → view results.
3. The panel shows granular permissions: Read, Write, Modify, attributes, extended permissions, etc.
4. Use **Show advanced permissions** to see the full list.

---
