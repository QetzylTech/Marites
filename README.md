# Minecraft Client and Server Setup
By JP

## Client TLDR
1. Install the latest:
  TLauncher https://tlauncher.org/en/
  Tailscale https://tailscale.com/download
2. Join VPN using the Tailscale account provided by JP
3. Import modpack 
  https://drive.google.com/drive/folders/1vuYmIkiJw5WnN9wqXW7krUkUowxOI1wr?usp=sharing
4. Join the server using the URL provided by JP
5. Read 1.1 and 1.2 for detailed instructions.

## Foreword
This documentation is intended for Marites only. Most instructions are aimed at the server admin.
It assumes all VPNs, tunnels, and credentials are distributed manually and are not public.
While the tutorial uses Cisco’s Modpacks, it can work with other Forge modpacks—adjust as needed (other modpacks are untested).
For best results, follow these instructions at least once while on a call with JP or Sam.
The majority of this guide covers server setup and configuration.

## Table of Contents

- [1 CLIENT SETUP](#1-client-setup)
  - [1.1 Install Modpack](#11-install-modpack)
  - [1.2 Joining VPN (If Required)](#12-joining-vpn-if-required)
  - [1.3 Connect to Server](#13-connect-to-server)
- [2 Server Setup](#2-server-setup)
  - [2.1 Create and Distribute Modpacks](#21-create-and-distribute-modpacks)
  - [2.2 Deploy Server (Windows)](#22-deploy-server-windows)
  - [2.3 Deploy Server (Ubuntu CLI)](#23-deploy-server-ubuntu-cli)
    - [2.3.1 Ubuntu Server Installation](#231-ubuntu-server-installation)
      - [A. Prepare Installation Media](#a-prepare-installation-media)
      - [B. Install Ubuntu Server](#b-install-ubuntu-server)
    - [2.3.2 Minecraft Server Deployment](#232-minecraft-server-deployment)
  - [2.4 Server Properties and Other Configs](#24-server-properties-and-other-configs)
  - [2.5 Network Setup (VPN Path)](#25-network-setup-vpn-path)
  - [2.6 Network Setup (Tunnel Path)](#26-network-setup-tunnel-path)
  - [2.7 Server Moderation](#27-server-moderation)
  - [2.8 Backup and Sync (WIP uwu)](#28-backup-and-sync-wip-uwu)
- [3 General Notes and Known Issues](#3-general-notes-and-known-issues)


## 1 CLIENT SETUP
Steps required for players to join the server.
### 1.1 Install Modpack
  1. Download the modpack zip from the folder provided by JP/Sam.
  2. Open TLauncher and go to the TLMod tab.
  3. Click the screwdriver & wrench icon and then select Backup Mods.
  4. Find the modpack zip and click Restore.
  5. Launch TLauncher with the restored modpack to ensure it loads successfully.
### 1.2 Joining VPN (If Required)
  Ask JP which VPN to use: Tailscale, ZeroTier, or Radmin.
  Install only 1 VPN.
#### 1.2.1 Tailscale
1. Install Tailscale from https://tailscale.com/download
2. Open Tailscale and log in with the account provided by JP.
3. Verify using your phone number if prompted.
4. Wait for OTP and authorization.
5. Confirm your device is listed as connected.
#### 1.2.2 ZeroTier
1. Install ZeroTier from https://www.zerotier.com/download/
2. Open ZeroTier from the tray.
3. Click “Join Network” and enter the network key provided by JP.
4. Wait for JP to approve your device.
5. Confirm your device shows as authorized in ZeroTier.
#### 1.2.3 Radmin
1. Refer to the Radmin setup instructions from Le Cafe.
2. Connect using the credentials provided by JP.
3. Confirm connection to the network.
#### Notes: 
- Each device must have the VPN client installed and authorized by the admin (JP)
- Up to 10 authorized devices (including the server) can access Zerotier
- Up to 3 accounts can connect to a network in Tailscale
- Uses a static ip address and port to connect
### 1.3 Connect to Server
1. Launch the modpack in TLauncher
2. In the main menu, select `Multiplayer` → `Add Server`.
3. Enter the server URL provided by JP.
4. Click Done, Join Server.
## 2 Server Setup
Steps required to develop, deploy, expose, and operate a server.
### 2.1 Create and Distribute Modpacks
Steps:
1. Open TLauncher and navigate to TLMods.
2. Select the modpack of your choice or  download your own set of mods.
3. Test run by launching the game.
4. Do necessary tweaks and optimizations
5. Export the modpack by clicking the screwdriver & wrench icon and then select Backup Mods.
6. Select Create Backup, choose the modpack, and then the save location.
7. Share the newly created zip file.
### 2.2 Deploy Server (Windows)
Preconditions:
- Java JDK installed (recommended version 17 for modded, 21 for vanilla).
- Modpack created and ready for distribution (See 2.1).
- Admin machine has sufficient resources for server.

Steps:
1. Create a folder for the server files (e.g., C:\MinecraftServer).
2. Download server jar:
    - Vanilla: from Mojang or Piston link.
    - Modded: Forge installer matching Minecraft version.
3. Install Forge (if modded):
    - Run the Forge installer → select `Server` → browse to server folder.
4. Run server jar once:
    - Double-click `server.jar` (vanilla) or `run.bat` (modded) to generate default files.
5. Accept EULA:
    - Open eula.txt → set eula=true.
6. Copy modpack files to server folder (modded only):
    - `mods/`, `config/`, `defaultconfigs/`, `scripts/`, `kubejs/`
    - Remove client-only mods (Oculus, LegendaryTooltips).
7. Adjust server startup script (optional):
  
    - Set RAM allocation: -Xms1024M -Xmx2048M.
8. Start server:
    - Double-click run.bat → verify console shows successful startup.
### 2.3 Deploy Server (Ubuntu CLI)
Skip to 2.3.2 If Ubuntu is already installed.
#### 2.3.1 Ubuntu Server Installation
Preconditions:
  - Target PC ready.
  - 8GB+ USB drive.
  - Ubuntu Server ISO downloaded.
  - Flashing tool ready (Rufus, Balena Etcher, etc.).

Steps:
##### A. Prepare Installation Media
1. Flash Ubuntu Server ISO to USB using your chosen tool.
2. Insert USB into target PC.
3. Boot from USB (adjust BIOS boot order if necessary).
##### B. Install Ubuntu Server
1. Follow installation prompts:
    - Select language and keyboard layout.
    - Create admin user (example: jp).
    - Accept all default options.
    - Do not install additional packages.
2. Complete installation and reboot into Ubuntu Server.
#### 2.3.2 Minecraft Server Deployment
Assuming Ubuntu Server is installed and booted, Modpack files prepared on client machine.
1. Create a folder for the server files using:
    <pre><code>
    mkdir MinecraftFolder
    </code></pre>
2. Run these commands to install Samba
    <pre><code>
    sudo apt update
    sudo apt install samba
    </code></pre>
3. Run the command to open the Samba config using Nano text editor:
    <pre><code>
    sudo nano /etc/samba/smb.conf
    </code></pre>
4. At the end of the file, append:
    <pre><code>
    [global] 
    workgroup = WORKGROUP 
    security = user 
    map to guest = never 
    server string = Samba Server 
    passdb backend = tdbsam 
    
    # Force modern authentication 
    client min protocol = SMB2 
    server min protocol = SMB2 
    ntlm auth = yes 
    
    [MinecraftFolder] 
    path = /home/jp/MinecraftFolder
    browseable = yes 
    read only = no 
    guest ok = no 
    valid users = jpazo
    </code></pre>
5. Press ctrl+o to save, ctrl+x to close Nano
6. Create an SMB password using this command:
    <pre><code>
    sudo smbpasswd -a jp
    </code></pre>
7. Restart smb using:
    <pre><code>
    sudo systemctl restart smbd nmbd
    </code></pre>
8. Run these commands to install ZeroTier and join a network
    <pre><code>
    sudo curl -s https://install.zerotier.com | sudo bash
    sudo zerotier-cli join <network_id>
    </code></pre>
9. Install JDK using these commands
    <pre><code>
    sudo apt update
    sudo apt install default-jdk
    </code></pre>
10. On Windows Explorer, where you created the modpack, type `\\ServerName` in the address bar to access the server.
11. Type in the username and password.
12. Open the shared folder and copy the files created using section 2.4.2.
13. After the file copy is finished, run the following:
    <pre><code>
    cd MinecraftFolder
    chmod a+x yourscript.sh
    ./run.sh
    </code></pre>
### 2.4 Server Properties and Other Configs
1. Open server.properties
   - Navigate to the server folder
   - Open `server.properties` in a text editor
2. Set server identity and world
   - Server name (displayed in server list): 
     `motd=Totally Chill Server`
   - World name (Also folder containing world files): `level-name=myworld`
   - World seed (applies only on first world generation): 
     `level-seed=69420018030897796`
3. Set player limits
   - Maximum number of players: `max-players=20`
4. Account and validation settings
   - Allow cracked/unofficial accounts: `online-mode=false`
   - Disable Mojang account validation to prevent registry sync fail: `enforce-secure-profile=false`
5. Optional gameplay and server settings
   - Adjust difficulty, game mode, PvP, spawn protection, and other options as desired
   - Enable whitelist (note: may not be fully effective if online-mode and enforce-secure-profile are false)
6. Save and close the file
   - Stop the server before saving changes
   - Keep a backup of `server.properties` for recovery
7. Verify settings
   - Restart the server
   - Confirm world loads with correct name/seed
   - Check that max players, MOTD, and account settings are applied correctly
   - Observe console for errors or warnings related to properties
8. Other configuration notes
   - Configs are the same for Windows and Ubuntu servers
   - Most admin functions can be done without OP privileges
   - Any additional mods or plugin configs should go in their respective folders (`mods/`, `config/`, `scripts/`) and be verified
   - Regularly backup server properties and world files
### 2.5 Network Setup (VPN Path)
Choose only 1 VPN
#### A. ZeroTier (Based on https://docs.zerotier.com/start)
1. Register a new account at https://www.zerotier.com/
2. Make a new network and open it
3. Set the ip address range to 192.168.192.xx
4. Download and install https://www.zerotier.com/download/
5. Open ZeroTier from the tray
6. Press join network and use the key provided by JP
7. Refresh your network view to see your new device.
8. Click the arrow-up icon on the left of the new device.
9. Set the device name, ip address of your choice (Within the range you chose), and check Authorize.
#### B. Radmin
  Refer to Le Cafe for Radmin setup.
#### C. Tailscale
1. Go to https://tailscale.com/download and install Tailscale
2. Log in to Tailscale using the account provided by JP
3. Verify using phone number
4. Wait for the otp.
#### Notes:
- Each device must have the VPN Client installed and authorized by the admin (JP)
- Up to 10 authorized devices (including the server) can access Zerotier
- Up to 3 accounts can connect to a network in Tailscale
- Static IP address
- Essentially simulates having everyone in the same house/ LAN
- Can be used for other purposes other than Minecraft.
### 2.6 Network Setup (Tunnel Path)
Choose only 1 Tunnel
##### A. Playit.gg
1. Register a new account at Playit.gg
2. Download and install Playit.gg app. Just follow the on-screen instructions (After installation, run it, and it will prompt you to follow a link)
3. Press Continue to add the server as an agent.
4. Rename your agent to something easy to remember. Press Add Agent.
5. Press Create Tunnel
6. On the region dropdown, select Global. Tunnel type is Minecraft Java. Ensure enable 
7. Assign the agent to a tunnel.
8. Once assigned, it will generate a url that you can share.
#### B. Ngrok
#### Notes:
- Only the server needs to be set up
- Anyone with the server url can access - less secure, DO NOT SHARE URL PUBLICLY
- Playit.gg has a randomly generated but persistent domain name/ url
- Double check ip addresses and port numbers. Make sure that Playit.gg has updated ports.
- Playit.gg has a glitch that causes connections to fail even with proper settings. Workaround is either set the port to something else and then set it back to the proper port, or unassign all agents, deactivate all tunnels, then reactivate 1 tunnel and reassign your agent.
- When the server is laggy, the only solution so far is switch between different services or swap servers.
- Tunnels essentially turn you into a public server without using port forwarding.
### 2.7 Server Moderation
- Refer to the Mojang website for server admin commands
- Enable whitelist; may not be fully effective since Mojang Account validation is disabled.
- Do not give op privileges to anyone unless absolutely necessary. Most admin functions can be done without op privilege.
### 2.8 Backup and Sync (WIP uwu)
## 3 General Notes and Known Issues
Common, observed problems and their usual causes.
- Use the Forge version for the Minecraft version of the modpack (Minecraft version indicated at the tlauncher modpack download page). Use the recommended versions of Forge, not the latest, unless you have a very specific reason.
- During installation, run the Forge jar by DOUBLE-CLICKING, NOT CMD. Using CMD will install to the default location: 'C:\Users\<YourUsername>\AppData\Roaming\.minecraft'
- Eula.txt will only show up if installation is successful.
- I said to copy just those folders in the instructions. I did that + copied everything in the tlauncher folder and it worked fine. Just need to delete oculus and legendarytooltips from the mod folder.
- If run.bat shows a terminal window running and then it outputs an error after loading the mods, you can see the cause on the first few lines of error after the list of mods (oculus error or something). Usually just means you need to delete client-side mods.
- If the server starts successfully, you should see a window with a graph and console.
- Whitelist is not very effective if online-mode and enforce-secure-profile in server.properties are both false. This is because anyone can just change usernames, and it won't be verified by the server.
- Make your own batch files so you don't have to open the terminal and type commands each time you start the server. Forge does this for you, but you can still edit the batch file.
- The arguments when starting the server, -Xms1024M and -Xmx2048M, set the max ram usage at startup and at runtime. If not set, the default value is 1/16 and 1/4 of the installed ram, respectively.
- I recommend applying the config below in the server.properties.
- Latest supported JDK version is 17 for modded and 21 for Vanilla. 24 works fine in testing, so far. If bugs appear, use the older JDK versions.
