# 🔐 Secure SSH Access and User Setup on Ubuntu Server

<p>Setting up secure SSH access is crucial for managing your Ubuntu server efficiently and securely. This guide walks you through the process of creating a secure **SSH key-based authentication system**, eliminating the need for password-based logins. By following this step-by-step tutorial, you will: </p>

✅ Set up a **new user (`ubuntu_user`)** for better security and access management  
✅ **Disable password authentication** and enable **key-based login** for improved security  
✅ **Ensure proper file permissions** and configuration settings to prevent unauthorized access  
✅ Learn how to **grant `sudo` privileges** to the `ubuntu_user` user (optional)  

By the end of this guide, you will have a **secure and robust** SSH authentication system that ensures only authorized users can access your server. 🚀  

---
## 📜 Table of Contents
1. [📖 Introduction](#-introduction)
2. [⚙️ Prerequisites](#️-prerequisites)
3. [💻 Local Device Setup](#-local-device-setup)
   - [🔑 Set Permissions for the `.pem` File](#-set-permissions-for-the-pem-file)
   - [🔐 Generate a Public Key from the Private Key](#-generate-a-public-key-from-the-private-key)
   - [📤 Copy the Public Key to the Server](#-copy-the-public-key-to-the-server)
   - [✅ Verify SSH Access as `ubuntu_user`](#-verify-ssh-access-as-ubuntu_user)
4. [🖥️ Ubuntu Server Setup](#%EF%B8%8F-ubuntu-server-setup)
   - [🔓 Log in to the Server as Root](#-log-in-to-the-server-as-root)
   - [👤 Create and Configure the `ubuntu_user` User](#-create-and-configure-the-ubuntu_user-user)
   - [📂 Set Up SSH Directory for `ubuntu_user`](#-set-up-ssh-directory-for-ubuntu_user)
   - [🔏 Configure Public Key Authentication](#-configure-public-key-authentication)
   - [⚡ Update SSH Configuration](#-update-ssh-configuration)
   - [🛠️ Grant `sudo` Privileges (Optional)](#%EF%B8%8F-grant-sudo-privileges-optional)

---

## 📖 Introduction  
This guide provides step-by-step instructions for configuring **secure SSH access** to an Ubuntu server using a `.pem` key. It includes setting up a new user (`ubuntu_user`), configuring SSH permissions, and enabling public key authentication.  

---

## ⚙️ Prerequisites  
✅ `.pem` key file (e.g., `key.pem`)  
✅ Ubuntu server with root access  
✅ SSH and SCP installed on the local machine  

---

# 💻 Local Device Setup  

## 🔑 Set Permissions for the `.pem` File  
```bash
chmod 400 key.pem
```

## 🔐 Generate a Public Key from the Private Key  
```bash
ssh-keygen -y -f key.pem > key.pub
```

## 📤 Copy the Public Key to the Server  
```bash
scp -i key.pem key.pub root@<server-ip>:/home/ubuntu_user/
```

## ✅ Verify SSH Access as `ubuntu_user`  
```bash
ssh -i key.pem ubuntu_user@<server-ip>
```

---

# 🖥️ Ubuntu Server Setup  

## 🔓 Log in to the Server as Root  
```bash
ssh -i key.pem root@<server-ip>
```

## 👤 Create and Configure the `ubuntu_user` User  
```bash
adduser ubuntu_user
su - ubuntu_user
```

## 📂 Set Up SSH Directory for `ubuntu_user`  
```bash
mkdir -p ~/.ssh
chmod 700 ~/.ssh
```

## 🔏 Configure Public Key Authentication  
```bash
cat /home/ubuntu_user/key.pub >> ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
rm /home/ubuntu_user/key.pub
chown -R ubuntu_user:ubuntu_user ~/.ssh
```

## ⚡ Update SSH Configuration  
Edit the SSH configuration file:  
```bash
nano /etc/ssh/sshd_config
```
Modify or add the following lines:  
```plaintext
PubkeyAuthentication yes
PasswordAuthentication no
```
Restart SSH:  
```bash
systemctl restart ssh
```

## 🛠️ Grant `sudo` Privileges (Optional) 
```bash
su - another_admin_user
sudo usermod -aG sudo ubuntu_user
```

---

🚀 Now ubuntu_user can securely access the server using the .pem key without a password! 🔥
🔑 Public Key Cryptography: Strong encryption, hard to break.
💻 No Password Storage: No password to intercept.
⚔️ Brute Force Protection: Harder to guess than passwords.
🕵️‍♂️ Keylogging Protection: No keystrokes to capture.
🔒 Complexity & Strength: Random, secure, long keys.
🛡️ Single-Use: Keys can be revoked, and sessions are short-lived.
🔒 Extra Protection: Option to add a passphrase for the private key.

🚀 More secure than passwords! 
