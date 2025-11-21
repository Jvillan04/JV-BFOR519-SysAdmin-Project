# Proxmox monitoring with Pulse

For monitoring, I’m using **Pulse**, an open-source monitoring platform built specifically for Proxmox VE, Proxmox Backup Server, Proxmox Mail Gateway, and Docker. It gives me a single dashboard where I can see node health, VM and LXC metrics, storage usage, and backup status across my whole lab in real time.

Pulse is designed for homelab admins and sysadmins who want **Proxmox-aware alerts** without having to flip between multiple UIs. It supports alerts and webhooks to tools like email, Discord, Slack, and Telegram, so I can get notified when nodes go down, containers misbehave, or storage is close to full. 

## Using Pulse in this project lets me:

- Treat Proxmox like a “real” production cluster with central monitoring
    
- Practice deploying and maintaining a dedicated monitoring service (Docker / VM)
    
- Have a clean “single pane of glass” view for my Proxmox and Docker infrastructure

## Installation Screenshots

> Installing Pulse
<img width="1260" height="731" alt="image" src="https://github.com/user-attachments/assets/79cefe67-3b3a-48c0-b9a3-98aa652a1cff" />

> Going through installation options
<img width="1260" height="731" alt="image" src="https://github.com/user-attachments/assets/385bcf58-401d-4304-b635-54f27cd1b541" />

> Install Complete (Also give you some important commands to remember in the output)
<img width="1260" height="731" alt="image" src="https://github.com/user-attachments/assets/9d9bd4e7-559b-41c0-bbb1-a616e5bc86c3" />

> Pulse container running
<img width="1286" height="749" alt="image" src="https://github.com/user-attachments/assets/618c2f15-6422-4fba-80fc-1a9269e25157" />


## Going to the Pulse monitoring WebGUI

> Note: With the use of Tailscale's subnet routing feature, it means I am able to remotely access this Pulse LXC without needing to install Tailscale on it. (Very useful)

> Going to the IP address in the image for the first time.
> Run the command needed to retrieve the token, This is for security purposes
<img width="1745" height="1024" alt="image" src="https://github.com/user-attachments/assets/91eb76b3-727e-4985-b57f-226eee94c8e5" />

> Running the command it needs (In Pulse LXC CLI)
<img width="1260" height="61" alt="image" src="https://github.com/user-attachments/assets/18ef64bd-ce9a-4bed-b036-5f24210b7a91" />

> Set the admin user
<img width="1745" height="1024" alt="image" src="https://github.com/user-attachments/assets/3f1d4112-f5ba-4f65-9576-49f86a29864a" />

> Adding the Proxmox Node, I set it to auto discover and it was able to find my Proxmox server on the network
<img width="1628" height="940" alt="image" src="https://github.com/user-attachments/assets/097d794d-e2ca-4233-9b11-16aa16cc57c9" />

> I need to install a service on my server to be able to communicate it's system information with the Pulse LXC and show it on the dashboard
<img width="680" height="1006" alt="image" src="https://github.com/user-attachments/assets/4c0f777a-751a-4632-ad7b-fb358ce7447b" />

The above is where we are actually setting up Pulse to monitor Proxmox, we run the command given to us by pulse as root in our proxmox server to set up the monitoring of this server.

> Registering our Proxmox server to Pulse (On Proxmox server CLI)
<img width="1260" height="731" alt="image" src="https://github.com/user-attachments/assets/8383ed57-6820-4e75-97ca-51a512ff0bbf" />

> We now go back to our dashboard and can see our Proxmox server has been added
<img width="1611" height="913" alt="image" src="https://github.com/user-attachments/assets/ba94148d-0a36-4510-a646-31aa239f94ff" />

> More Detailed view of what is running in our Proxmox server
<img width="1581" height="640" alt="image" src="https://github.com/user-attachments/assets/782d9bc5-cf71-4b29-89c9-07a15eaf15e8" />

> We can also see alerts now too. This one of from some VMs that were powered off after a brief power outage
<img width="1611" height="753" alt="image" src="https://github.com/user-attachments/assets/e258ad96-e5d8-4d9d-b7bb-c9ac99513a31" />

> We can also view our alerts history to see past alerts
<img width="1687" height="1019" alt="image" src="https://github.com/user-attachments/assets/ec03ec12-a11d-4d30-b7b0-18c059733b3c" />









