# Secure SSH Access Setup

## Prerequisites
- Ubuntu Server
- `.pem` Key File
- SSH and SCP Installed

## Steps

### Local Device
1. **Set Permissions for the `.pem` File**  
   ```bash
   chmod 400 Phi-Mysql-Export.pem
   ```

2. **Generate Public Key**  
   ```bash
   ssh-keygen -y -f Phi-Mysql-Export.pem > Phi-Mysql-Export.pub
   ```

3. **Copy Public Key to Server**  
   ```bash
   scp -i Phi-Mysql-Export.pem Phi-Mysql-Export.pub root@<server-ip>:/home/devops/
   ```

4. **Verify SSH Access**  
   ```bash
   ssh -i Phi-Mysql-Export.pem devops@<server-ip>
   ```

### Ubuntu Server
5. **Log in as Root**  
   ```bash
   ssh -i Phi-Mysql-Export.pem root@<server-ip>
   ```

6. **Create `devops` User**  
   ```bash
   adduser devops
   su - devops
   ```

7. **Set Up SSH Directory**  
   ```bash
   mkdir -p ~/.ssh
   chmod 700 ~/.ssh
   ```

8. **Configure Authentication**  
   ```bash
   cat /home/devops/Phi-Mysql-Export.pub >> ~/.ssh/authorized_keys
   chmod 600 ~/.ssh/authorized_keys
   rm /home/devops/Phi-Mysql-Export.pub
   chown -R devops:devops ~/.ssh
   ```

9. **Update SSH Configuration**  
   ```bash
   nano /etc/ssh/sshd_config
   ```
   Add or modify the following lines:
   ```plaintext
   PubkeyAuthentication yes
   PasswordAuthentication no
   ```
   Restart SSH service:
   ```bash
   systemctl restart ssh
   ```

10. **Grant `sudo` Privileges (Optional)**  
   ```bash
   su - another_admin_user
   sudo usermod -aG sudo devops
   ```

Now `devops` can securely access the server using the `.pem` key without a password!
