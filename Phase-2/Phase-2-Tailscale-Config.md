# Adding Tailscale to Proxmox

## Step 1: Create an LXC Container on Proxmox for Tailscale

1. Create a new LXC container in Proxmox.
2. Set the hostname (e.g., `tailscale-lxc`).
3. Select **Unprivileged container** for better security.
4. Set a password for the `root` user.
5. Choose an Ubuntu template (e.g., `22.04`).
6. Leave disk size at the default (8 GB) since we do not need much.
7. Set CPU to **1 core** and memory to **512 MB**.
8. Configure the network to **DHCP** initially.
9. Confirm the settings and tick **Start after created** before finishing.



## Step 2: Enable SSH Connection

1. Log in to the LXC container’s console as `root`.
2. Edit the SSH configuration file:

   ```bash
   nano /etc/ssh/sshd_config
   ```

3. Change:

   ```text
   PermitRootLogin prohibit-password
   ```

   to:

   ```text
   PermitRootLogin yes
   ```

4. Save (`Ctrl+O`, `Enter`) and exit (`Ctrl+X`).

5. Restart SSH:

   ```bash
   systemctl restart ssh
   ```

---

## Step 3: Change to a Static IP

1. Find the container’s current IP address:

   ```bash
   ip a
   ```

2. In the Proxmox web GUI, go to the LXC container’s **Network** settings.

3. Change IPv4/CIDR from **DHCP** to **Static** and enter the IP address obtained (e.g., `192.168.1.187/24`).

4. Set the gateway (e.g., `192.168.1.1`).

5. Verify the network by pinging an external site:

   ```bash
   ping google.com
   ```

---

## Step 4: Update / Upgrade and Install `curl`

1. SSH into the LXC container from your terminal using the static IP.

2. Update and upgrade the system:

   ```bash
   sudo apt update && sudo apt upgrade -y
   ```

3. Install `curl`:

   ```bash
   sudo apt install curl -y
   ```

---

## Step 5: Install Tailscale

1. Go to the Tailscale installation guide for Linux:
   [https://tailscale.com/download/](https://tailscale.com/download/)
2. Copy the installation script provided for Ubuntu/Debian.
3. Paste the script into your SSH terminal and press **Enter** to install Tailscale.

---

## Step 6: Extra Settings for Tailscale in an Unprivileged Container

### 6.1 Enable IPv4/IPv6 Forwarding

1. Edit `sysctl.conf`:

   ```bash
   sudo nano /etc/sysctl.conf
   ```

2. Uncomment or add the following lines:

   ```text
   net.ipv4.ip_forward=1
   net.ipv6.conf.all.forwarding=1
   ```

3. Save (`Ctrl+O`, `Enter`) and exit (`Ctrl+X`).

4. Apply the changes:

   ```bash
   sudo sysctl -p
   ```

5. Shut down the LXC container:

   ```bash
   sudo shutdown now
   ```

### 6.2 Mount `/dev/net/tun` in Proxmox

1. In the Proxmox web GUI, select your Proxmox server (`pve`).

2. Open the **Shell**.

3. Edit the container’s configuration file (replace `YOUR_CONTAINER_ID`):

   ```bash
   nano /etc/pve/lxc/YOUR_CONTAINER_ID.conf
   # example:
   # nano /etc/pve/lxc/101.conf
   ```

4. Add these two lines at the end of the file:

   ```bash
   lxc.cgroup2.devices.allow: c 10:200 rwm
   lxc.mount.entry: /dev/net/tun dev/net/tun none bind,create=file
   ```

5. Save (`Ctrl+O`, `Enter`) and exit (`Ctrl+X`).

6. Start the LXC container again from the Proxmox GUI.

---

## Step 7: Start Tailscale with Subnet Advertising and Exit Node

1. SSH back into the LXC container.

2. Run the `tailscale up` command with advertising flags (replace with your network):

   ```bash
   sudo tailscale up --advertise-routes=192.168.1.0/24 --advertise-exit-node
   ```

3. Copy the URL printed in the terminal.

4. Open the URL in your web browser and log in with your Tailscale account (e.g., Google).

5. Connect the device to your Tailscale network.

6. Verify the connection:

   ```bash
   tailscale status
   ```

---

## Step 8: Approve Subnet Routes and Exit Node in Tailscale Admin Console

1. Go to [https://tailscale.com/admin/machines](https://tailscale.com/admin/machines) and log in.
2. Find your newly added device in the list.
3. Click the **three dots** next to the device and select **Edit route settings**.
4. Enable **Subnet routes** (e.g., `192.168.1.0/24`) and **Use as exit node**.
5. Optionally, disable **Key expiry** for this device from the same menu if you want it to stay connected long-term.

```
```
