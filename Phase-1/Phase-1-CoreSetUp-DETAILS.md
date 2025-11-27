# Phase 1 - Install Details

These notes and screenshots are mainly for my own reference. They show how I installed Proxmox VE on the server and got the web UI address.

_Note: This is how I installed Proxmox on my hardware. Steps can change depending on the system you are installing Proxmox on._

---

## Getting Proxmox onto a drive

Download the Proxmox VE ISO from the Proxmox site and flash it to a USB drive using a tool like Balena Etcher or Rufus. These tools write image files to storage devices and prepare the installer for your server.

<img width="389" height="251" alt="image" src="https://github.com/user-attachments/assets/ed81c7c8-0b4e-47d8-a41c-308c1dc8e8b8" />

Once the USB is ready, plug it into your server.

---

## Booting from the installer

Plug the USB drive with the Proxmox installer into the server USB port. Power on the system and enter the boot menu by pressing the key your hardware uses, such as F12, F11, or Esc. Select the USB drive as the boot device to start the Proxmox installer.

> Startup screen when booting the Proxmox installer  
<img width="1044" height="788" alt="pve-grub-menu" src="https://github.com/user-attachments/assets/1cb3a258-bc05-492e-b8d0-624eb3ce769e" />

Follow the on screen setup prompts to install Proxmox onto your main storage drive. During the install, you set up the IP address for the server. Later you use that address to access the web UI from another device:

```text
https://<server_IP>:8006
```

When the installation completes, remove the USB drive and take note of the web interface address shown on the final screen. This is how you access the Proxmox dashboard from another device.

You should see a summary screen similar to this. The IP address and drive info may differ. This is a sample screen since at the time of writing these steps were already completed.

<img width="1044" height="788" alt="pve-install-summary" src="https://github.com/user-attachments/assets/1705a985-9deb-4cc8-bf81-a0857bc7a835" /> ```

You can name them something like Phase-1-results.md and Phase-1-details.md and link from the results file if you want. Want a one line link added at the top of the results file that points to the details file?
