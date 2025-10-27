# Adding Tailscale to Proxmox

## Step 1: Create an LXC container on Proxmox for Tailscale 

    Create a new LXC container in Proxmox.
    Set the hostname (e.g., tailscale-LXC).
    Select "unprivileged container" for better security.
    Set a password for the root user.
    Choose an Ubuntu template (e.g., 22.04).
    Leave disk size at default (8GB) we don't need much.
    Set CPU to 1 core and memory to 512MB.
    Configure the network to DHCP initially.
    Confirm settings and tick "Start after created" before finishing.

## Step 2: Enable SSH Connection

    Log in to the LXC container's console as root.
    Edit the SSH configuration file: nano /etc/ssh/sshd_config
    Change PermitRootLogin prohibit-password to PermitRootLogin yes.
    Save (Ctrl+O, Enter) and exit (Ctrl+X).

  
## Step 3: Changing to Static IP

    Find the container's current IP address by typing ip a in the console.
    In the Proxmox web GUI, go to the LXC container's "Network" settings.
    Change the IPv4/CIDR from DHCP to "Static" and enter the IP address obtained (e.g., 192.168.1.187/24).
    Set the Gateway (e.g., 192.168.1.1).
    Verify the network by pinging an external site (e.g., ping google.com).

## Step 4: Update and Upgrade Process & Install Curl

    SSH into the LXC container from your terminal using the static IP.
    Update and upgrade the system: sudo apt update && sudo apt upgrade -y
    Install curl: sudo apt install curl -y

## Step 5: Tailscale Install

    Go to the Tailscale installation guide for Linux (link: https://tailscale.com/download/https://tailscale.com/download/).
    Copy the installation script provided.
    Paste the script into your SSH terminal and press Enter to install Tailscale.

## Step 6: Extra Settings for Tailscale to Work (Unprivileged Container)

    Enable IPv4 Forwarding:
        Edit sysctl.conf: sudo nano /etc/sysctl.conf
        Uncomment net.ipv4.ip_forward=1 and net.ipv6.conf.all.forwarding=1.
        Save (Ctrl+O, Enter) and exit (Ctrl+X).
    Shut down the LXC container: sudo shutdown now
    Mount /dev/net/tun:

        In the Proxmox web GUI, select your Proxmox server (PVE).

        Open the "Shell".

        Edit the container's configuration file: `nano /etc/pve/lxc/YOUR_CONTAINER_ID.conf` (e.g., nano /etc/pve/lxc/101.conf).

        Add these two lines at the end of the file:
        ```bash
        lxc.cgroup2.devices.allow: c 10:200 rwm
        lxc.mount.entry: /dev/net/tun dev/net/tun none bind,create=file
        ```
        Save (Ctrl+O, Enter) and exit (Ctrl+X).
    Start the LXC container.

## Step 7: Start Tailscale Service with Subnet Advertising and Exit Node
    SSH back into the LXC container.
    Run the Tailscale up command with advertising flags: sudo tailscale up `--advertise-routes=YOUR_LOCAL_NETWORK_CIDR --advertise-exit-node`
    Replace YOUR_LOCAL_NETWORK_CIDR with your actual local network, e.g., `192.168.1.0/24`.
    Copy the URL provided in the terminal.
    Open the URL in your web browser and log in with your Tailscale account (e.g., Google).
    Connect the device to your Tailscale network.
    Verify connection by typing tailscale status in the terminal.

## Step 8: Approve Subnet Advertising and Exit Node in Tailscale Admin Console 

    Go to https://tailscale.com/admin/machines and log in.
    Find your newly added device in the list.
    Click the three dots next to the device and select "Edit route settings".
    Enable "Subnet routes" (e.g., 192.168.1.0/24) and "Use as exit node".
    Optionally, disable "Key expiry" for this device from the same menu.

