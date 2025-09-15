# JV-BFOR519-SysAdmin-Project
## Proxmox + Tailscale + Home Assistant + JetBrains Gateway

### Secure, remote-friendly homelab:

- Proxmox host for VMs and LXC containers

- Private remote access with Tailscale

- Home Assistant dashboard to view VM/LXC status and alerts

- Remote IDE workflow with JetBrains Gateway as thin client and JetBrains IDEs hosted on VMs/LXCs

## Goals

- Set up a Proxmox server you can reach securely from anywhere

- See VM and container health at a glance

- Get notified when something goes wrong

Work on code through a remote IDE with low local hardware needs
```mermaid
Architecture
flowchart LR
  subgraph Internet
    Client[Thin client<br/>JetBrains Gateway]
  end

  subgraph Tailnet[Tailscale private network]
    PVE[Proxmox Host]
    HA[Home Assistant VM/LXC]
    DEV[Dev VM/LXC with SSH]
  end

  Client <--> |Tailscale| PVE
  Client <--> |Tailscale| DEV
  HA <--> |Proxmox API| PVE
```

## Stack

- Proxmox VE (host)

- Tailscale (private mesh VPN, SSH, HTTPS certs)

- Home Assistant (dashboard and alerts)

- JetBrains Gateway (remote IDE access to a dev VM/LXC)

## Prerequisites

- Proxmox VE installed and reachable on your local network

- A Tailscale account

- Basic Linux familiarity (SSH, apt)
