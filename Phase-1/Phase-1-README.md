# Phase 1 - Core Set Up

## Proxmox foundation

### What Proxmox is and how it fits this project

Proxmox VE is an open-source virtualization platform that lets you run virtual machines and LXC containers on a single physical server. It has a web interface, role-based access control, snapshots, and backups, so it feels close to a production hypervisor.

In this project, Proxmox is the base layer. Later phases will sit on top of it:
- Tailscale will handle secure remote access into the lab.
- Pulse will monitor the Proxmox node and workloads.
- A dev VM/LXC will host my development tools, and I can expand to more services (n8n, Minecraft, etc.).

Getting Proxmox installed and reachable is the first step before adding any of those pieces.

## What I did in Phase 1

Phase 1 was focused on a clean Proxmox install:

- Prepared the hardware and Proxmox VE installer.
- Installed Proxmox VE on the host machine.
- Set a static IP so the Proxmox web UI is reachable on my local network.
- Logged into the Proxmox web interface as `root@pam` and verified that the node is online and ready to host VMs and containers.

The goal here was not to run any workloads yet, only to get a stable hypervisor in place that I can build on.


_Note: The below is just what I did to get Proxmox Up and running. Things could be different depending on the system that you are instaling Proxmox in_

## Getting Proxmox on a drive
Download the Proxmox VE ISO from the Proxmox site and flash it to a USB drive using a tool like Balena Etcher (or Rufus), which is a tool for writing image files to storage devices. This prepares the installer for your server.

<img width="389" height="251" alt="image" src="https://github.com/user-attachments/assets/ed81c7c8-0b4e-47d8-a41c-308c1dc8e8b8" />

Once the USB is ready, plug it into your server.


## Insert the drive into the server
Plug the USB drive with the Proxmox installer into your server’s USB port. Power on the system and enter the boot menu (usually by pressing a key like F12, F11, or Esc, depending on your hardware). Select the USB drive as the boot device to start the Proxmox installer.

> Your screen at start up should look like this:
<img width="1044" height="788" alt="pve-grub-menu" src="https://github.com/user-attachments/assets/1cb3a258-bc05-492e-b8d0-624eb3ce769e" />

Follow the on-screen setup prompts to install Proxmox onto your main storage drive. This includes setting up the IP address for the server, which you'll later use to access it remotely from your PC using:
```
http://<server_IP>:8006.
```

Once installation completes, remove the USB drive and take note of the web interface address shown on the final screen (this is how you’ll access the Proxmox dashboard from another device).

You should see a summary screen similar to this (your IP address and drive info may differ. Note: This is not my device, since at the time of writing these steps were completed prior):
<img width="1044" height="788" alt="pve-install-summary" src="https://github.com/user-attachments/assets/1705a985-9deb-4cc8-bf81-a0857bc7a835" />



## Results and what is next

Below is a screenshot of the Proxmox web interface showing the node online and ready:

> **Figure 1.** Proxmox VE web UI after a successful install.
<img width="1751" height="1023" alt="image" src="https://github.com/user-attachments/assets/c43ebd95-5199-4868-b2ee-3e6e2987a0ed" />


With Phase 1 complete, the system now has a working virtualization layer. This sets the stage for the next steps:

- Create a dev VM/LXC that will act as my central development server.
- Install Tailscale so I can reach Proxmox and the dev VM securely from outside my home network.
- Later phases will add monitoring with Pulse and set up JetBrains Gateway to use the dev VM as a remote IDE host.

Phase 1 is the base: a working Proxmox host that I can turn into a full homelab platform in the next phases.
