# Secure SSH Access Setup

## Prerequisites
- Ubuntu Server
- `.pem` Key File
- SSH and SCP Installed

## Steps

### Local Device

#### Step 1: Set Permissions for the `.pem` File
```bash
chmod 400 Phi-Mysql-Export.pem
```

#### Step 2: Generate Public Key
```bash
ssh-keygen -y -f Phi-Mysql-Export.pem > Phi-Mysql-Export.pub
```

#### Step 3: Copy Public Key to Server
```bash
scp -i Phi-Mysql-Export.pem Phi-Mysql-Export.pub root@<server-ip>:/home/devops/
```

#### Step 4: Verify SSH Access
```bash
ssh -i Phi-Mysql-Export.pem devops@<server-ip>
```

---

### Ubuntu Server

#### Step 5: Log in as Root
```bash
ssh -i Phi-Mysql-Export.pem root@<server-ip>
```

#### Step 6: Create `devops` User
```bash
adduser devops
su - devops
```

#### Step 7: Set Up SSH Directory
```bash
mkdir -p ~/.ssh
chmod 700 ~/.ssh
```

#### Step 8: Configure Authentication
```bash
cat /home/devops/Phi-Mysql-Export.pub >> ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
rm /home/devops/Phi-Mysql-Export.pub
chown -R devops:devops ~/.ssh
```

#### Step 9: Update SSH Configuration
```bash
nano /etc/ssh/sshd_config
```
Modify or add:
```plaintext
PubkeyAuthentication yes
PasswordAuthentication no
```
Restart SSH:
```bash
systemctl restart ssh
```

#### Step 10: Grant `sudo` Privileges (Optional)
```bash
su - another_admin_user
sudo usermod -aG sudo devops
```

Now `devops` can securely access the server using the `.pem` key without a password!
