# Phase 1 - Core Set Up



## Getting Proxmox on a drive
Download the Proxmox VE ISO from the Proxmox site and flash it to a USB drive using a tool Balena Etcher (or Rufus), which is a tool for writing image files to storage devices. This prepares the installer for your server.

<img width="389" height="251" alt="image" src="https://github.com/user-attachments/assets/ed81c7c8-0b4e-47d8-a41c-308c1dc8e8b8" />

Once the USB is ready, plug it into your server.


## Insert the drive into the server
Plug the USB drive with the Proxmox installer into your server’s USB port. Power on the system and enter the boot menu (usually by pressing a key like F12, F11, or Esc, depending on your hardware). Select the USB drive as the boot device to start the Proxmox installer.

Your screen at start up should look like this:
<img width="1044" height="788" alt="pve-grub-menu" src="https://github.com/user-attachments/assets/1cb3a258-bc05-492e-b8d0-624eb3ce769e" />

Follow the on-screen setup prompts to install Proxmox onto your main storage drive. This includes setting up the IP address for the server, which you'll later use to access it remotely from your PC using:
```
http://<server_IP>:8006.
```

Once installation completes, remove the USB drive and take note of the web interface address shown on the final screen (this is how you’ll access the Proxmox dashboard from another device).

You should see a summary screen similar to this (your IP address and drive info may differ):
<img width="1044" height="788" alt="pve-install-summary" src="https://github.com/user-attachments/assets/1705a985-9deb-4cc8-bf81-a0857bc7a835" />
