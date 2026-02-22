# Linux VPS Hardening

## Overview

This project documents the provisioning and security hardening of a Linux VPS hosted on Hostinger. The goal was to reduce attack surface and implement best-practice server security controls. This project was completed as part of my self-directed infrastructure learning outside of formal coursework.

## Architecture

![Infrastructure Overview](architecture/architecture_diagram.png)

## Environment

Hosting Provider: Hostinger VPS

OS: (Ubuntu 22.04)

SSH Client: Termius

Firewall: UFW

Intrusion Prevention: Fail2Ban

## Security Measures Implemented
### SSH Hardening

- Generated SSH key pair
- Disabled password authentication
- Disabled root login
- Enforced key-based authentication only

### Firewall Configuration

- Allowed inbound SSH (port 22) and denied all other unsolicited inbound traffic by default.
- Enabled UFW logging
- Blocked all unnecessary inbound traffic
- Verified active rules using ufw status

### Brute-Force Protection

- Installed Fail2Ban
- Configured sshd jail
- Verified jail status using:
    `sudo fail2ban-client status`

## Why These Controls Matter

- SSH key authentication prevents brute-force password attacks
- Firewall reduces exposed services
- Fail2Ban automatically bans malicious IPs
- Disabling root login limits privilege escalation risk

## Verification

### Confirmed UFW status:
- Default: deny (incoming), allow (outgoing)
- Active rules validated using: sudo ufw status verbose

### Confirmed Fail2Ban:
- sshd jail active
- Verified monitoring of /var/log/auth.log
- Checked ban status using: sudo fail2ban-client status sshd

### Verified effective SSH configuration using:
- `sudo sshd -T | grep permitrootlogin`
- `sudo sshd -T | grep passwordauthentication`

## Lessons Learned

- Importance of verifying logs
- Understanding how authentication logs trigger Fail2Ban
- Real-world server hardening practices

## Future Improvements

- Implement WireGuard VPN for secure remote access
- Configure automatic security updates
- Add system monitoring (e.g., Prometheus/Grafana)
- Enable log rotation and centralized logging
