# **Windows Server 2022 Installation Notes**

## Goal

Install Windows Server 2022 in an Oracle VirtualBox virtual machine, then complete basic post-installation setup.

## Requirements

- Oracle VirtualBox (the video uses version 7.1.4) - https://www.virtualbox.org/
- Windows Server 2022 64-bit ISO - https://www.microsoft.com/en-us/evalcenter/download-windows-server-2022
- Windows 11 ISO, if needed for a separate virtual machine

## 1. Download the software

1. Download and install Oracle VirtualBox.
2. Download the 64-bit Windows Server 2022 ISO from Microsoft.
3. To create a Windows 11 ISO, download Microsoft’s Windows 11 installation media tool:
    1. Run the tool.
    2. Accept the recommended options, or choose the appropriate options for your PC.
    3. Select **ISO file** and save it.
    
    <img width="1916" height="912" alt="image" src="https://github.com/user-attachments/assets/a12bf595-eb69-4fe9-94f5-5e6dd9e34321" />
    

## 2. Create the virtual machine

1. In VirtualBox, select **New**.

<img width="940" height="667" alt="image 1" src="https://github.com/user-attachments/assets/dc672332-21c4-4aee-acfe-54449510b0df" />

1. Name the VM **Server 2022**.
2. Select the Windows Server 2022 operating-system type/version.
3. In the VM settings, assign:
    - **Processors:** 2 CPUs
    - **Memory:** 8 GB (the presenter considers 4–8 GB)
    
    <img width="758" height="537" alt="image 2" src="https://github.com/user-attachments/assets/ae760293-3b5b-4c73-a881-09e35aaefc36" />
    
4. Save the settings and start the VM.
5. When prompted for installation media, select the Windows Server 2022 ISO.

## 3. Install Windows Server

1. Proceed through the Windows Setup screens.

<img width="681" height="517" alt="image 3" src="https://github.com/user-attachments/assets/89427cc3-5780-4dea-9202-08ae3626dadd" />
1. Select the edition that includes **Desktop Experience** to install the graphical interface.
    - The edition without Desktop Experience is Server Core and has no standard Windows desktop.
    
   <img width="691" height="514" alt="image 4" src="https://github.com/user-attachments/assets/79b8ed30-a538-42c9-9bb9-d3f8d7383977" />
    
2. Choose **Custom** installation.
3. Select the virtual disk and continue.
    - In a production environment, disk formatting and partitioning may require a planned configuration. This walkthrough uses the default disk setup.
4. Wait for installation and any initial updates to finish. The VM may restart during this process.

## 4. Complete initial setup

1. After installation, set the Administrator password.

<img width="687" height="460" alt="image 5" src="https://github.com/user-attachments/assets/2594359e-482c-4c77-8fc3-e468a0a7b9f0" />

1. Send **Ctrl+Alt+Delete** to the VM to sign in.
    - In VirtualBox, use **Input → Keyboard → Insert Ctrl+Alt+Delete** if needed.
2. Eject or remove the installation ISO from the virtual optical drive so the VM does not boot from it again.

## 5. Adjust time and display

1. Open the date and time settings.
2. Set the correct time zone for your location.
3. Adjust the VirtualBox display scaling or virtual screen resolution to suit your needs.

## 6. Shut down or restart

Windows command examples:

- Open the shutdown dialog: `shutdown /i`
- Shut down: `shutdown /s`
- Restart: `shutdown /r`
- Display help: `shutdown /?`

You can also shut down Windows through its normal power options.
