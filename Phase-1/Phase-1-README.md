# Phase 1 - Core Set Up
Download the Proxmox VE ISO and flash it to a USB drive using Balena Etcher, a simple tool for writing image files to storage devices. This prepares the installer for your server.

## Getting Proxmox on a drive
Once the USB is ready, plug it into your server and boot from it. Use the Proxmox installer to set up the host OS on the system drive. After installation, note the IP address assigned so you can manage Proxmox from the web UI.


## Insert the drive into the server
Plug the USB drive with the Proxmox installer into your server’s USB port. Power on the system and enter the boot menu (usually by pressing a key like F12, F11, or Esc depending on your hardware). Select the USB drive as the boot device to start the Proxmox installer.
Follow the on‑screen setup prompts to install Proxmox onto your main storage drive. Once installation completes, remove the USB drive and note the web interface address shown on screen — this will be used later to access the Proxmox dashboard from another device.

Your screen at start up should look like this
<img width="1044" height="788" alt="pve-grub-menu" src="https://github.com/user-attachments/assets/1cb3a258-bc05-492e-b8d0-624eb3ce769e" />

Once the install is complete it you should have a little summary of your settings (These are not my setting but I had the same screen with a different IP and drive settings but overall the same)
<img width="1044" height="788" alt="pve-install-summary" src="https://github.com/user-attachments/assets/1705a985-9deb-4cc8-bf81-a0857bc7a835" />
