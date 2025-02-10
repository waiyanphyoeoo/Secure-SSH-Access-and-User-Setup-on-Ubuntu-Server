
readme_emoji_detailed = """# 🔐 Secure SSH Access and User Setup on Ubuntu Server

Setting up secure SSH access is crucial for managing your Ubuntu server efficiently and securely. This guide walks you through the process of creating a secure **SSH key-based authentication system**, eliminating the need for password-based logins. By following this step-by-step tutorial, you will:  

✅ Set up a **new user (`devops`)** for better security and access management  
✅ **Disable password authentication** and enable **key-based login** for improved security  
✅ **Ensure proper file permissions** and configuration settings to prevent unauthorized access  
✅ Learn how to **grant `sudo` privileges** to the `devops` user (optional)  

By the end of this guide, you will have a **secure and robust** SSH authentication system that ensures only authorized users can access your server. 🚀  

---
## 📜 Table of Contents
1. [📖 Introduction](#-introduction)
2. [⚙️ Prerequisites](#️-prerequisites)
3. [💻 Local Device Setup](#-local-device-setup)
   - [🔑 Set Permissions for the `.pem` File](#-set-permissions-for-the-pem-file)
   - [🔐 Generate a Public Key from the Private Key](#-generate-a-public-key-from-the-private-key)
   - [📤 Copy the Public Key to the Server](#-copy-the-public-key-to-the-server)
   - [✅ Verify SSH Access as `devops`](#-verify-ssh-access-as-devops)
4. [🖥️ Ubuntu Server Setup](#-ubuntu-server-setup)
   - [🔓 Log in to the Server as Root](#-log-in-to-the-server-as-root)
   - [👤 Create and Configure the `devops` User](#-create-and-configure-the-devops-user)
   - [📂 Set Up SSH Directory for `devops`](#-set-up-ssh-directory-for-devops)
   - [🔏 Configure Public Key Authentication](#-configure-public-key-authentication)
   - [⚡ Update SSH Configuration](#-update-ssh-configuration)
   - [🛠️ Grant `sudo` Privileges (Optional)](#-grant-sudo-privileges-optional)

---

## 📖 Introduction  
This guide provides step-by-step instructions for configuring **secure SSH access** to an Ubuntu server using a `.pem` key. It includes setting up a new user (`devops`), configuring SSH permissions, and enabling public key authentication.  

---

## ⚙️ Prerequisites  
✅ `.pem` key file (e.g., `Phi-Mysql-Export.pem`)  
✅ Ubuntu server with root access  
✅ SSH and SCP installed on the local machine  

---

# 💻 Local Device Setup  

## 🔑 Set Permissions for the `.pem` File  
```bash
chmod 400 Phi-Mysql-Export.pem
```

## 🔐 Generate a Public Key from the Private Key  
```bash
ssh-keygen -y -f Phi-Mysql-Export.pem > Phi-Mysql-Export.pub
```

## 📤 Copy the Public Key to the Server  
```bash
scp -i Phi-Mysql-Export.pem Phi-Mysql-Export.pub root@<server-ip>:/home/devops/
```

## ✅ Verify SSH Access as `devops`  
```bash
ssh -i Phi-Mysql-Export.pem devops@<server-ip>
```

---

# 🖥️ Ubuntu Server Setup  

## 🔓 Log in to the Server as Root  
```bash
ssh -i Phi-Mysql-Export.pem root@<server-ip>
```

## 👤 Create and Configure the `devops` User  
```bash
adduser devops
su - devops
```

## 📂 Set Up SSH Directory for `devops`  
```bash
mkdir -p ~/.ssh
chmod 700 ~/.ssh
```

## 🔏 Configure Public Key Authentication  
```bash
cat /home/devops/Phi-Mysql-Export.pub >> ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
rm /home/devops/Phi-Mysql-Export.pub
chown -R devops:devops ~/.ssh
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
sudo usermod -aG sudo devops
```

---

🚀 Now devops can securely access the server using the .pem key without a password! 🔥
🔑 Public Key Cryptography: Strong encryption, hard to break.
💻 No Password Storage: No password to intercept.
⚔️ Brute Force Protection: Harder to guess than passwords.
🕵️‍♂️ Keylogging Protection: No keystrokes to capture.
🔒 Complexity & Strength: Random, secure, long keys.
🛡️ Single-Use: Keys can be revoked, and sessions are short-lived.
🔒 Extra Protection: Option to add a passphrase for the private key.

🚀 More secure than passwords! 
