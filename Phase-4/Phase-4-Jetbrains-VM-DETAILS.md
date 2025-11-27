# Phase 4 – JetBrains Gateway dev VM

## Goal

Set up a JetBrains dev VM in Proxmox that I can reach over Tailscale and use as a remote IDE backend through JetBrains Gateway. The idea is to keep all code and tools on the server while I use my laptop as a thin client.

---

## Steps taken

1. Created an Ubuntu Server VM in Proxmox  
   * Downloaded the Ubuntu Server ISO from the Ubuntu site.  
   * Uploaded the ISO to Proxmox storage and created a new VM named `jetbrains`.  
   * Gave the VM extra CPU and RAM so it would be comfortable for programming tasks.  

2. Installed Ubuntu Server and base tools  
   * Installed Ubuntu Server on the VM and created my user account.  
   * Updated the system packages after install.  

3. Added the VM to my Tailnet  
   * Installed Tailscale on the Ubuntu VM using the same install command as in Phase 1.  
   * Logged in from the VM and joined it to my Tailnet.  
   * Confirmed the VM shows up in the Tailscale admin page and that it is reachable over Tailscale.  

4. Set up Git and pulled my code  
   * Installed Git and the GitHub CLI on the VM.  
   * Ran `gh auth login` and signed into GitHub from the VM.  
   * Created a folder for my code, changed into that folder, and did a `git pull` to bring my project onto the VM.  
   * Note: You could also connect with JetBrains Gateway first, open an empty folder on the VM, and use the IDE GUI to clone or pull the repo into that folder. I chose the CLI flow because it makes it easier to see what Git is doing and helps you get comfortable with GitHub outside of the GUI.  

5. Installed JetBrains Gateway on my laptop  
   * Installed the JetBrains Gateway app on my laptop.  
   * Confirmed my laptop can see the JetBrains VM over Tailscale.  

6. Connected to the VM from JetBrains Gateway  
   * Opened JetBrains Gateway on my laptop and connected to the Ubuntu VM over SSH through Tailscale.  
   * Selected WebStorm as the IDE for TypeScript and JavaScript development.  
   * Logged into the VM from Gateway with the same username and password I set up during the Ubuntu install.  

7. Opened my project in the remote IDE  
   * In WebStorm, opened the project folder that I pulled from GitHub.  
   * Let WebStorm index the project and verified that navigation, IntelliSense, and other IDE features work from the laptop while the backend runs on the VM.  

---

## Results

The JetBrains dev VM now works as a remote IDE backend:

* From my laptop, I can open JetBrains Gateway and connect to the Ubuntu VM over Tailscale.  
* WebStorm runs on the VM as the backend while the JetBrains client runs on my laptop.  
* My project opens from the folder I pulled with Git, and I can edit, run, and debug code from the laptop without keeping a local copy of the repo.  
* The VM stays on my Tailnet, so it is not directly exposed to the public internet.  

Screenshots in this phase show:

* The JetBrains VM in Proxmox.  
* The VM listed in my Tailscale admin console.  
* JetBrains Gateway connected to the VM from my laptop.  
* WebStorm open with my project on the remote VM.  

These screenshots serve as the main “results” evidence for the phase.

---

## Notes

With this setup I can keep all of my tools and source code on the Proxmox server and still work comfortably from a lower power laptop. It also keeps my development traffic inside the Tailnet instead of exposing extra ports on the public internet.
