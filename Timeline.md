## Phase 1 - Core Setup (Oct 15 – Oct 27)

**Goal: Get Proxmox running and ready for services**

  - Install Proxmox VE on server

  - Test connection to Proxmox to see if it is accessible
  
  - Create empty VMs and LXC containers for later set up

## Phase 2 - Secure Access & Networking (Oct 28 – Nov 10)

**Goal: Enable private access via Tailscale**

   - Install Tailscale on Proxmox and any VMs/Containers I want to access remotely

   - Set up MagicDNS and test SSH/HTTPS access
     
   - Configure tailscale cert + cron for Proxmox UI

## Phase 3 - Monitoring & Automation (Nov 11 – Nov 24)

**Goal: Add monitoring with Pulse**
  - Install Pulse in LXC or VM

  - Integrate with Proxmox API to monitor VMs/LXCs

## Phase 4 - Remote IDE  (Nov 25 – Dec 3)

**Goal: Enable coding from anywhere & finalize project**

   - Install JetBrains Gateway on local machine (PC)

   - Connect to hosted IDE in Proxmox container/VM

   - Test remote IDE
