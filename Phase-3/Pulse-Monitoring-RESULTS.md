# Proxmox monitoring with Pulse

**Outcome:** Pulse is now monitoring my Proxmox host and guests and sending useful alerts, so I have a central view of my lab instead of only using the Proxmox UI.

For monitoring, I am using **Pulse**, an open source monitoring platform built for Proxmox VE, Proxmox Backup Server, Proxmox Mail Gateway, and Docker. It gives me a single dashboard where I can see node health, VM and LXC metrics, storage usage, and backup status for my lab in real time.

Pulse is designed for homelab admins and sysadmins who want Proxmox aware alerts without having to flip between multiple UIs. It supports alerts and webhooks to tools like email, Discord, Slack, and Telegram, so I can get notified when nodes go down, containers misbehave, or storage is close to full.

Using Pulse in this project lets me:

* Treat Proxmox like a real production cluster with central monitoring  
* Practice deploying and maintaining a dedicated monitoring service in its own LXC  
* Have a single view for my Proxmox and Docker infrastructure  

---

## Results: Pulse monitoring Proxmox

These screenshots show Pulse actually monitoring my Proxmox server and giving useful views and alerts.

> Adding the Proxmox node. I set it to auto discover and it was able to find my Proxmox server on the network  
<img width="1628" height="940" alt="image" src="https://github.com/user-attachments/assets/097d794d-e2ca-4233-9b11-16aa16cc57c9" />

> Pulse tells me to install a service on the Proxmox server so it can send system information to the Pulse LXC  
<img width="680" height="1006" alt="image" src="https://github.com/user-attachments/assets/4c0f777a-751a-4632-ad7b-fb358ce7447b" />

I then ran the command from Pulse as `root` on the Proxmox host to register it with Pulse.

> Registering the Proxmox server to Pulse from the Proxmox CLI  
<img width="1260" height="731" alt="image" src="https://github.com/user-attachments/assets/8383ed57-6820-4e75-97ca-51a512ff0bbf" />

> Back on the Pulse dashboard, I can see my Proxmox server added and reporting in  
<img width="1611" height="913" alt="image" src="https://github.com/user-attachments/assets/ba94148d-0a36-4510-a646-31aa239f94ff" />

> More detailed view of what is running on my Proxmox server  
<img width="1581" height="640" alt="image" src="https://github.com/user-attachments/assets/782d9bc5-cf71-4b29-89c9-07a15eaf15e8" />

> Alerts view. Here you can see alerts from VMs that were powered off after a brief power outage  
<img width="1611" height="753" alt="image" src="https://github.com/user-attachments/assets/e258ad96-e5d8-4d9d-b7bb-c9ac99513a31" />

> Alert history view to see past alerts over time  
<img width="1687" height="1019" alt="image" src="https://github.com/user-attachments/assets/ec03ec12-a11d-4d30-b7b0-18c059733b3c" />

---

## Summary

With Pulse in place, I now have:

* A dedicated monitoring LXC for my Proxmox environment  
* A web dashboard that shows node status, VM and LXC metrics, and storage usage  
* Alerts for issues like powered off VMs after a power outage  

This makes my Proxmox homelab feel closer to a monitored production setup and ties in well with the rest of the project.
