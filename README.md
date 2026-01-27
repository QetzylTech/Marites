# Minecraft Client and Server Setup
By JP

Tutorial is for for Cisco's Modpacks but can work with other forge modpacks, modify accordingly (Steps not tested with other modpacks, though).

Recommended to follow these at least once while in call with JP or Sam.
## Client TLDR
1. Install TLauncher
2. Join VPN (ZeroTier/Tailscale)
3. Import modpack zip
4. Join server using provided URL
## Table of Contents
- [1. CLIENT SETUP](#1-client-setup)
  - [1.1. Tunnel/ VPN](#11-tunnel-vpn)
    - [1.1.1. ZeroTier (Based on https://docs.zerotier.com/start)](#111-zerotier-based-on-httpsdocszerotiercomstart)
    - [1.1.2. Tailscale](#112-tailscale)
    - [1.1.3. Radmin](#113-radmin)
    - [1.1.4. Notes](#114-notes)
  - [1.2. Installing Modpacks](#12-installing-modpacks)
  - [1.3. Connecting to Server](#13-connecting-to-server)
- [2. SERVER SETUP](#2-server-setup)
  - [2.1. Tunnel](#21-tunnel)
    - [2.1.1. Playit.gg](#211-playitgg)
    - [2.1.2. Ngrok](#212-ngrok)
    - [2.1.3. Notes](#213-notes)
  - [2.2. VPN](#22-vpn)
    - [2.2.1 ZeroTier (Based on https://docs.zerotier.com/start)](#221-zerotier-based-on-httpsdocszerotiercomstart)
    - [2.2.2 Radmin](#222-radmin)
    - [2.2.3 Tailscale](#223-tailscale)
    - [2.2.4 Notes](#224-notes)
  - [2.3. Installing Vanilla Server](#23-installing-vanilla-server)
  - [2.4. Installing Modded Server](#24-installing-modded-server)
    - [2.4.1 Installing Modded Server](#241-installing-modded-server)
    - [2.4.2 Installing Modpacks](#242-installing-modpacks)
  - [2.5. Starting Server](#25-starting-server)
  - [2.6. Notes](#26-notes)
- [3. Ubuntu Server Deployment](#3-ubuntu-server-deployment)
  - [3.1. Ubuntu Server Installation](#31-ubuntu-server-installation)
  - [3.2. Setup](#32-setup)
    - [3.2.1 Server Folder](#321-server-folder)
    - [3.2.2 Samba](#322-samba)
    - [3.2.3 Tunnel/ VPN](#323-tunnel-vpn)
  - [3.3. Installing Modded Server](#33-installing-modded-server)
  - [3.4. Server Startup](#34-server-startup)
- [4. Server Configuration](#4-server-configuration)
  - [4.1. Server Properties](#41-server-properties)
  - [4.2. Server Rules](#42-server-rules)
  - [4.3. File Sync and Backup](#43-file-sync-and-backup)
- [5. Server Automation](#5-server-automation)
  - [5.1. Scripts](#51-scripts)

## 1. CLIENT SETUP
### 1.1. **Tunnel/ VPN**
#### 1.1.1. **ZeroTier (Based on https://docs.zerotier.com/start)**
1. Download and install https://www.zerotier.com/download/
2. Open ZeroTier from tray
3. Press join network and use the key provided by JP
4. Wait for JP to approve you
5. On minecraft, join server address 192.168.192.99:25565
(If previously installed, just wait for JP to give you updated ip address and port number)
#### 1.1.2. **Tailscale**
1. Go to https://tailscale.com/download and install Tailscale
2. Login to Tailscale using the account provided by JP
3. Verify using phone number
4. Wait for the otp.
#### 1.1.3. **Radmin**
#### 1.1.4. **Notes**
- Each device must have the VPN client installed and authorized by admin (JP)
- Up to 10 authorized devices (including the server) can access Zerotier
- Up to 3 accounts can connect to a network in Tailscale
- Uses static ip address and port to connect
### 1.2. **Installing Modpacks**
1. Download the modpack zip file that Sam/ JP sends you
2. Open Tlauncher and then open the TLmod tab
3. On the upper left part of the window, click the screwdriver and wrench icon and select Backup Mods.
4. Find the  mod zip file you downloaded and click restore.
5. Launch the game.
### 1.3. **Connecting to Server**
1. JP/ Sam gives you url.
2. On Minecraft, join the server using the url
## 2. SERVER SETUP
### 2.1. **Tunnel**
#### 2.1.1. **Playit.gg**
1. Register new account at Playit.gg
2. Download and install Playit.gg app. Just follow the on-screen instructions (After installation, run it and it will prompt you to follow a link)
3. Press Continue to add server as agent.
4. Rename your agent to something easy to remember. Press add Agent.
5. Press Create Tunnel
6. On the region dropdown, select Global. Tunnel type is Minecraft Java. Ensure enable 
7. Assign the agent to a tunnel.
8. Once assigned, it will generate a url that you can share.
#### 2.1.2. **Ngrok**
#### 2.1.3. **Notes**
- Only the server needs setup
- Anyone with the server url can access - less secure, DO NOT SHARE URL PUBLICLY
- Playit.gg has a randomly generated but persistent domain name/ url
- Double check ip addresses and port numbers. Make sure that Playit.gg has updated ports.
- Playit.gg has a glitch that causes connections to fail even with proper settings. Workaround is either set the port to something else and then set it back to the proper port, or unassign all agents, deactivate all tunnels, then reactivate 1 tunnel and reassign your agent.
- When server is laggy, only solution so far is switch between different services, or swap server.
- Tunnels essentially turns you into a public server without using port forwarding.
### 2.2. **VPN**
#### 2.2.1 **ZeroTier (Based on https://docs.zerotier.com/start)**
1. Register new account at https://www.zerotier.com/
2. Make a new network and open it
3. Set the ip address range to 192.168.192.xx
4. Download and install https://www.zerotier.com/download/
5. Open ZeroTier from tray
6. Press join network and use the key provided by JP
7. Refresh your network view to see your new device.
8. Click the arrow up icon on the left of the new device.
9. Set the device name, ip address of your choice (Within the range you chose), and check authorize.
#### 2.2.2 **Radmin***
#### 2.2.3 **Tailscale**
1. Go to https://tailscale.com/download and install Tailscale
2. Login to Tailscale using the account provided by JP
3. Verify using phone number
4. Wait for the otp.
#### 2.2.4. **Notes**
- Each device must have the VPN Client installed and authorized by admin (JP)
- Up to 10 authorized devices (including the server) can access Zerotier
- Up to 3 accounts can connect to a network in Tailscale
- Static IP address
- Essentially simulates having everyone in the same house/ LAN
- Can be used for other purposes other than Minecraft.
### 2.3. **Installing Vanilla Server**
1. Install Java JDK from here: https://www.oracle.com/java/technologies/downloads/
2. Download the minecraft server jar. 1.21.1 available here: https://piston-data.mojang.com/v1/objects/6bce4ef400e4efaa63a13d5e6f6b500be969ef81/server.jar
3. Make a folder where you will place the server. Move the jar file to that folder.
4. Open cmd in that folder.
5. Run: 
    <pre><code>
    java -jar server.jar. 
    </pre></code>
    After running, it will generate some files and folders. Including **eula.txt**
6. Open **eula.txt** and find the line that says eula=false. Set it to true.
7. To start the server, run: 
    <pre><code>
    java -jar server.jar --nogui, 
    </pre></code>
    Or if you want to set the start and max ram usage: 
    <pre><code>
    java -Xms1024M -Xmx2048M -jar server.jar --nogui
    </pre></code>
### 2.4. **Installing Modded Server**
#### 2.4.1 **Installing Modded Server**
0. Install Java JDK from here: https://www.oracle.com/java/technologies/downloads/
1. Download and install Cisco's Modpack in Tlauncher, run at least once but don't make a world.
2. Download forge-1.20.1-47.4.0-installer.jar from https://files.minecraftforge.net/net/minecraftforge/forge/
3. Create a new, empty folder for your server.
3. Run the downloaded jar file by double clicking. Select server and browse to the empty folder where you want to install forge and the modpack
4. After installation, open the Forge folder and double click run.bat. 
5. Eula will be generated, set eula=true.
#### 2.4.2 **Installing Modpacks**
1. On TLauncher, install the mods or modpack  of your choice.
2. On File Explorer, navigate to the tlauncher minecraft directory containing the '/mod' and '/config' folders
3. Copy the tlauncher modpack files to the Forge folder. Important folders are: 'mods/', 'config/', 'defaultconfigs/' (if present), 'scripts/' or 'kubejs/' (optional), 
4. Remove client-only mods like: oculus, legendarytooltips, etc.
### 2.5. **Starting Server**
To start the server, double click run.bat
### 2.6. **Notes**
- Use the Forge version for the Minecraft version of the modpack (Minecraft version indicated at tlauncher modpack download page). Use the recommended versions of Forge, not the latest, unless you have a very specific reason.
- During installation, run forge jar by DOUBLE CLICKING, NOT CMD. Using cmd will install to the default location: 'C:\Users\<YourUsername>\AppData\Roaming\.minecraft'
- Eula.txt will only show up if installation is successful.
- I said to copy just those folders in the instruction. I did that + copied everything in the tlauncher folder and it worked fine. Just need to delete oculus and legendarytooltips from mod folder.
- If run.bat shows a terminal window running and then it outputs an error after loading the mods, you can see the cause on the first few lines of error after the list of mods (oculus error or something). Usually just means, you need to delete client side mods.
- If server starts successfully, you should see a window with a graph and console.
- Whitelist is not very effective if online-mode and enforce-secure-profile in server.properties are both false. This is because anyone can just change usernames and it won't be verified by the server.
- Make your own batch files so you don't have to open terminal and type commands each time you start the server. Forge does this for you, but you can still edit the batch file.
- The arguments when starting the server, -Xms1024M and -Xmx2048M, sets the max ram usage at startup and at runtime. If not set, the default value is 1/16 and 1/4 of installed ram, respectively.
- I recommend applying the config below in the server.properties.
- Latest supported JDK version is 17 for modded and 21 for Vanilla. 24 works fine in testing, so far. If bugs appear, use the older JDK versions.
## 3. Ubuntu Server Deployment 
### 3.1. **Ubuntu Server Installation**
1. Download Ubuntu Server ISO from Canonical's website
2. Burn the ISO to an 8GB or larger flash drive using a flashing tool (e.g. Rufus, Balena Etcher)
3. Plug in the flash drive to the target pc and boot from it. Change BIOS boot order as needed.
4. Select the default options in the installation. Do not install any  additional packages. For the next steps, username "jp" will be used as an example.
### 3.2. **Setup**
#### 3.2.1. **Server  Folder**
Create a folder for the server files using:
    <pre><code>
        mkdir MinecraftFolder
    </pre></code>
#### 3.2.2. **Samba**
1. Run these commands to install Samba
    <pre><code>
    sudo apt update
    sudo apt install samba
    </pre></code>
2. Run the command to open Samba config using Nano text editor:
    <pre><code>
    sudo nano /etc/samba/smb.conf
    </pre></code>
3. At the end of the file, append:
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
4. Press ctrl+o to save, ctrl+x to close Nano
5. Create an SMB password using this command:
    <pre><code>
    sudo smbpasswd -a jp
    </pre></code>
6. Restart smb using:
    <pre><code>
    sudo systemctl restart smbd nmbd
    </pre></code>
#### 3.2.3. **Tunnel/ VPN**
Run these commands to install ZeroTier and join a network
    <pre><code>
    sudo curl -s https://install.zerotier.com | sudo bash
    sudo zerotier-cli join <network_id>
    </pre></code>
### 3.3. **Installing Modded Server**
1. Install JDK using these commands
    <pre><code>
    sudo apt update
    sudo apt install default-jdk
    </pre></code>
2. On Windows Explorer where you created the modpack, type '\\ServerName' on the address bar to access the server.
3. Type in the username and password.
4. Open the shared folder and copy here files created using section 2.4.2.
### 3.4. **Server Startup**
After file copy is finished, run the following:
    <pre><code>
    cd MinecraftFolder
    chmod a+x yourscript.sh
    ./run.sh
    </pre></code>
## 4. Server Configuration
### 4.1. **Server Properties**
- Open the file: server.properties
- To allow cracked/ unofficial accounts, look for online-mode=true and set it to false.
- To prevent registry sync fail due to Mojang account validation: enforce-secure-profile=false
- To set the server name, set motd= to the server name you want. (Example: motd=Totally Chill Server)
- To set world name: level-name=myworld
- To set world seed (Only applicable during 1st run/ world generation, seed to na sinend ni Den - village sa baba surrounded by cherry blossoms): level-seed=69420018030897796
- To set max number of players, max-players=20
### 4.2. **Server Rules**
- Refer to Mojang website for server admin commands
- Enable whitelist; may not be fully effective since Mojang Account validation is disabled.
- Do not give op privileges to anyone unless absolutely necessary. Most admin functions can be done without op privilege.
### 4.3. **File Sync and Backup**
1. Install Google Drive Desktop
2. Login using the account provided by JP
## 5. Server Automation
### 5.1. **Scripts**
WIP uwu

[⬆ Back to Top](#table-of-contents)
