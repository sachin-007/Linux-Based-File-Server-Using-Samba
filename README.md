# Linux Based File Server Using Samba

## Overview

This project sets up a Linux-based file server using Samba, allowing file sharing across a network. Samba enables Linux systems to communicate with Windows systems using the SMB/CIFS protocol.

## Prerequisites

- A Linux machine (e.g., Ubuntu) with root or sudo access.
- Basic knowledge of the Linux command line.

## Installation and Configuration

### 1. Install Samba

Run the following commands to install Samba:

```bash
# Update the package list
sudo apt update
```

# Install Samba

```bash
sudo apt install samba
```
### 2. Configure Samba
# Backup the Original Configuration File:
```bash
sudo cp /etc/samba/smb.conf /etc/samba/smb.conf.bak
```
# Edit the Samba Configuration File:
```bash
sudo nano /etc/samba/smb.conf
```

[Shared]
path = /srv/samba/shared
browseable = yes
writable = yes
guest ok = no
read only = no
create mask = 0644
directory mask = 0755

### 3. Create the Shared Directory

```bash
sudo mkdir -p /srv/samba/shared
sudo chmod 2775 /srv/samba/shared
sudo chown nobody:nogroup /srv/samba/shared
```
### 4. Create Samba Users
## 1. Add a New User to the System

```bash
sudo adduser sambauser
```
## 2. Set a Samba Password for the User:
```bash
sudo smbpasswd -a sambauser
```
### 5. Adjust Permissions

#Set Directory Ownership and Permissions
```bash
sudo chown sambauser:sambauser /srv/samba/shared
sudo chmod 2775 /srv/samba/shared
```

### 6. Adjust Permissions
#Restart the Samba Service:
```bash
sudo systemctl restart smbd
```
#Verify Samba Status:
```bash
sudo systemctl status smbd
```
### 6. Access the Shared Directory
##From Another Linux Machine:
#Use smbclient to access the shared directory:
```bash
smbclient //server-ip/Shared -U sambauser
```
#Replace 'server-ip' with the IP address of your Samba server
##From a Windows Machine:
#Open File Explorer and enter the server’s IP address:
```bash
\\server-ip\Shared
```
###8. Automate Samba Service on Startup
##Enable Samba to Start on Boot:
```bash
sudo systemctl enable smbd
```
