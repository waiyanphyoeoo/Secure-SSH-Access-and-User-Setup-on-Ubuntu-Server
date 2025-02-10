# Security Policy

## Overview

This repository provides a guide for securely setting up SSH access to an Ubuntu server using a `.pem` key for authentication. The setup enhances the security of the server by eliminating the need for passwords and protecting against common attack vectors such as brute-force attacks and keylogging.

## Recommended Security Practices

### 1. **SSH Key Authentication**
   - Always use SSH key-based authentication rather than password authentication to secure SSH access.
   - Use a `.pem` private key to authenticate securely without exposing your password.

### 2. **Public Key Cryptography**
   - Use strong encryption for key pairs (e.g., 2048-bit or higher RSA keys).
   - Protect the private key with a strong passphrase for an additional layer of security.
   
### 3. **Disable Password Authentication**
   - Set `PasswordAuthentication no` in the SSH configuration to ensure that only key-based authentication is allowed.

### 4. **Limit Root Login**
   - Disable direct root login by setting `PermitRootLogin no` in the `/etc/ssh/sshd_config` file. Instead, use a regular user account with sudo privileges.

### 5. **Firewall and Access Control**
   - Use a firewall (e.g., `ufw`, `iptables`) to restrict SSH access to trusted IP addresses.
   - Consider using fail2ban to automatically block IP addresses with too many failed login attempts.

### 6. **Use a Strong Passphrase for the Private Key**
   - Always encrypt your private key with a passphrase to prevent unauthorized access if the private key is compromised.
   
### 7. **SSH Configuration Hardening**
   - Enforce the use of strong ciphers and algorithms by adjusting the SSH configuration file (`/etc/ssh/sshd_config`).
   - Regularly update your SSH software to patch security vulnerabilities.

### 8. **Key Management**
   - Regularly rotate and revoke SSH keys that are no longer in use.
   - Use key management tools for better handling and tracking of SSH keys across multiple users.

### 9. **Monitor Server Access**
   - Regularly review SSH login logs located in `/var/log/auth.log` for suspicious activity.
   - Set up an intrusion detection system (IDS) to monitor for malicious login attempts.

## Reporting Security Vulnerabilities

If you discover a security vulnerability, please report it by creating an issue in this repository. Please follow the Responsible Disclosure process, and do not publicly disclose the vulnerability until a fix has been made.

