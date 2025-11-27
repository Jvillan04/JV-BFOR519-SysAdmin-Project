# Phase 3 - Pulse Install Details

These notes and screenshots are mainly for my own reference. They show how I installed Pulse in an LXC and how I first logged into the web GUI and linked Proxmox.

---

## Installation screenshots

These screenshots show the main steps of installing Pulse in an LXC and getting the service running.

> Installing Pulse  
<img width="1260" height="731" alt="image" src="https://github.com/user-attachments/assets/79cefe67-3b3a-48c0-b9a3-98aa652a1cff" />

> Going through installation options  
<img width="1260" height="731" alt="image" src="https://github.com/user-attachments/assets/385bcf58-401d-4304-b635-54f27cd1b541" />

> Install complete (the script also prints some important commands to remember)  
<img width="1260" height="731" alt="image" src="https://github.com/user-attachments/assets/9d9bd4e7-559b-41c0-bbb1-a616e5bc86c3" />

> Pulse container running in Proxmox  
<img width="1286" height="749" alt="image" src="https://github.com/user-attachments/assets/618c2f15-6422-4fba-80fc-1a9269e25157" />

---

## Accessing the Pulse web GUI

Thanks to Tailscale subnet routing, I can reach the Pulse LXC remotely without installing Tailscale inside that container. I only need Tailscale on my Proxmox host and my client device.

> First time going to the Pulse IP in a browser. The page asks for a token and shows the command needed to retrieve it for security  
<img width="1745" height="1024" alt="image" src="https://github.com/user-attachments/assets/91eb76b3-727e-4985-b57f-226eee94c8e5" />

> Running the token command inside the Pulse LXC  
<img width="1260" height="61" alt="image" src="https://github.com/user-attachments/assets/18ef64bd-ce9a-4bed-b036-5f24210b7a91" />

> Setting the admin user in the Pulse web GUI  
<img width="1745" height="1024" alt="image" src="https://github.com/user-attachments/assets/3f1d4112-f5ba-4f65-9576-49f86a29864a" />

---

## Linking Proxmox to Pulse

These steps connect the Proxmox host to Pulse so it can send system information and metrics.

> Adding the Proxmox node. I set it to auto discover and it was able to find my Proxmox server on the network  
<img width="1628" height="940" alt="image" src="https://github.com/user-attachments/assets/097d794d-e2ca-4233-9b11-16aa16cc57c9" />

> Pulse tells me to install a service on the Proxmox server so it can send system information to the Pulse LXC  
<img width="680" height="1006" alt="image" src="https://github.com/user-attachments/assets/4c0f777a-751a-4632-ad7b-fb358ce7447b" />

I then ran the command from Pulse as `root` on the Proxmox host to register it with Pulse.

> Registering the Proxmox server to Pulse from the Proxmox CLI  
<img width="1260" height="731" alt="image" src="https://github.com/user-attachments/assets/8383ed57-6820-4e75-97ca-51a512ff0bbf" />
