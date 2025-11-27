# Phase 1 Proxmox foundation

**Outcome:** Proxmox VE is installed on the host with a static IP and the web UI is reachable, so the server is ready to host VMs and containers for the later phases.

---

## What Proxmox is and how it fits this project

Proxmox VE is an open source virtualization platform that lets you run virtual machines and LXC containers on a single physical server. It has a web interface, role based access control, snapshots, and backups, so it feels close to a production hypervisor.

In this project, Proxmox is the base layer. Later phases will sit on top of it:

- Tailscale will handle secure remote access into the lab.  
- Pulse will monitor the Proxmox node and workloads.  
- A dev VM or LXC will host my development tools, and I can expand to more services like n8n or Minecraft.  

Getting Proxmox installed and reachable is the first step before adding any of those pieces.

---

## What I did in Phase 1

Phase 1 was focused on a clean Proxmox install:

- Prepared the hardware and Proxmox VE installer.  
- Installed Proxmox VE on the host machine.  
- Set a static IP so the Proxmox web UI is reachable on my local network.  
- Logged into the Proxmox web interface as `root@pam` and verified that the node is online and ready to host VMs and containers.  

The goal here was not to run any workloads yet, only to get a stable hypervisor in place that I can build on.

---

## Result screenshot

Below is a screenshot of the Proxmox web interface showing the node online and ready.

> Proxmox VE web UI after a successful install  
<img width="1751" height="1023" alt="image" src="https://github.com/user-attachments/assets/c43ebd95-5199-4868-b2ee-3e6e2987a0ed" />

---

## What is next

With Phase 1 complete, the system now has a working virtualization layer. This sets the stage for the next steps:

- Install Tailscale so I can reach Proxmox and the dev VM securely from outside my home network.  
- Create a dev VM or LXC that will act as my central development server.  
- Add monitoring with Pulse and set up JetBrains Gateway so I can use the dev VM as a remote IDE host.  

Phase 1 is the base: a working Proxmox host that I can turn into a full homelab platform in the next phases.
