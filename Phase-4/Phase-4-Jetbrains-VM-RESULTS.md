# JetBrains dev VM results

**Outcome:** The JetBrains dev VM now works as a remote IDE backend that I can reach over Tailscale and use from a lower power PC.

---

## Results

The JetBrains dev VM now works as a remote IDE backend:

* From my PC, I can open JetBrains Gateway and connect to the Ubuntu VM over Tailscale.  
* WebStorm runs on the VM as the backend while the JetBrains client runs on my PC.  
* My project opens from the folder I pulled with Git, and I can edit, run, and debug code from the PC without keeping a local copy of the repo.  
* The VM stays on my Tailnet, so it is not directly exposed to the public internet.  

---

## Screenshots

Screenshots in this phase show:

> The JetBrains VM in Proxmox  
<img width="1428" height="782" alt="image" src="https://github.com/user-attachments/assets/f906dbf1-c13d-4f84-9f20-31f727e09885" />

> The VM listed in my Tailscale admin console  
<img width="1210" height="854" alt="image" src="https://github.com/user-attachments/assets/bb5ae8c5-4e88-406e-bc6c-9e09cb026b99" />

> JetBrains Gateway connected to the VM from my PC  
<img width="1901" height="396" alt="image" src="https://github.com/user-attachments/assets/d4a3498f-bb32-4c76-aaf0-22fe34e9a0dd" />

> WebStorm open with my project on the remote VM  
<img width="1879" height="992" alt="image" src="https://github.com/user-attachments/assets/5cbd816a-9872-49cf-a769-54a72a9e637e" />


The project shown above is a TypeScript project I worked on. Now I can edit this wherever I am as long as I am on Tailscale and have the JetBrains Gateway app on my PC.

---

## Notes

With this setup I can keep all of my tools and source code on the Proxmox server and still work comfortably from a low power PC. It also keeps my development traffic inside the Tailnet instead of exposing extra ports on the public internet.

## Why this matters as a sysadmin

Setting up a JetBrains dev VM is useful from a sysadmin point of view because it lets you:

* Keep all dev tools and code in one controlled place instead of on many personal machines  
* Apply updates, patches, and security settings once on the VM instead of managing every developer PC  
* Reuse the same access controls, backups, and monitoring that already exist for the Proxmox host  
* Limit exposure by keeping SSH and IDE access inside the Tailnet instead of opening ports on the public internet  
* Support remote work with thin clients, since the heavy CPU and RAM use happens on the server  
* Reduce “it works on my machine” issues, because everyone who uses the dev VM shares the same environment
* * Show one example of a service you can run on a server, with many more you can add later depending on what you need  

This turns the dev environment into a managed service instead of a collection of individual laptops and shows how the same server can host other services in the future.
