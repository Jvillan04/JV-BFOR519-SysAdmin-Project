# Tailscale Results
After installing and configuring Tailscale on my Proxmox LXC container, and installing the Tailscale client on my Windows laptop, I am now able to successfully tunnel into my home server using Tailscale and my Tailscale domain name.

> Here is a screenshot of my tailscale container running in Proxmox
<img width="1595" height="765" alt="image" src="https://github.com/user-attachments/assets/073ab75e-a358-4881-9e17-680a74b8156e" />

> Here is a screenshot of my tailscale LXC container in my admin console
<img width="1055" height="663" alt="image" src="https://github.com/user-attachments/assets/c090c9cc-6a7a-4547-a2fa-1ad7f57e9993" />

> Here is a screenshot of my laptop on my admin console
<img width="1153" height="788" alt="image" src="https://github.com/user-attachments/assets/9f1cae70-9fc3-49bc-8857-316600293f94" />


## The connection process.

1. I make sure I am connected to the Tailscale client on my PC.

<img width="418" height="301" alt="image" src="https://github.com/user-attachments/assets/62dd3465-c5a3-48a4-90d5-f24a94609823" />

2. In my browser I enter
   ```text
   https://pve.humpback-mine.ts.net/#v1:0:18:4:::::::
   ```
   This points to my Proxmox server over the Tailscale network.

<img width="696" height="120" alt="image" src="https://github.com/user-attachments/assets/77ad3631-312e-45c3-b0ee-324ff4488ebb" />

3. I hit Enter and log into Proxmox as I normally would with my regular Proxmox credentials.

> Below is a screenshot of the system logs for my main Proxmox server. You can see the tailscaled daemon is running along with some other system info.
<img width="1910" height="815" alt="image" src="https://github.com/user-attachments/assets/d98f749f-0100-4c57-b0a1-5ca42d749145" />


## Trying it when the tailscale client is off
Now I test what happens when the Tailscale client is turned off on my laptop.

> Tailscale client turned off on my laptop
<img width="403" height="250" alt="image" src="https://github.com/user-attachments/assets/43fb1d60-29f9-42a2-a1d2-b8c1881e3458" />

> I go into the browser and enter the same address as before:
<img width="1915" height="983" alt="image" src="https://github.com/user-attachments/assets/5b76ac22-2963-4077-8887-376277758189" />

This time, the Proxmox web GUI fails to load. Since the Tailscale client is not running, my laptop cannot establish a secure tunnel to my home network and cannot reach the Proxmox server. This confirms that access is protected and only works when a device is properly connected to the Tailscale network.

## Why This Matters for the Project and as a Sysadmin

Having Tailscale running on my Proxmox server means I can securely reach my homelab from anywhere with an internet connection, without exposing ports on my router or using complex VPN hardware. For this project, it lets me treat Proxmox like a central development and management server that I can reach from low-power devices (like a laptop) from home, school, or anywhere else.

### From a system administration perspective, this setup shows a practical way to:

- Provide secure remote access to critical infrastructure.

- Avoid manual VPN configuration and port forwarding.

- Keep services behind a private overlay network (a virtual network that runs on top of your existing network) instead of the public internet.

- Maintain a simple way to manage and monitor remote machines through a single access path.

In short, Tailscale turns my Proxmox host into a securely reachable core of my lab, which is exactly what I need for a remote-friendly sysadmin environment.
