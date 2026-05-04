# Ubuntu systemd Service Recovery Lab

## Overview

This repository documents troubleshooting scenarios involving failed services on Ubuntu systems using `systemd`, `journalctl`, and service-specific validation tools.

The purpose of this project is to practice diagnosing and recovering failed services in a Linux support environment.

## Scenario

A user reports that a web application is unavailable. Investigation shows that the related service is either failed, disabled, misconfigured, or not listening on the expected port.

## Objectives

- Check service status
- Review service logs
- Identify failed units
- Validate service configuration
- Restart and enable services
- Confirm listening ports
- Verify application access
- Document root cause and resolution

## Environment

- OS: Ubuntu Server
- Service Examples: Nginx, Apache, SSH, custom systemd service
- Tools: `systemctl`, `journalctl`, `ss`, `curl`, `nginx -t`, `apache2ctl configtest`

## Skills Demonstrated

- `systemd` service troubleshooting
- Log analysis with `journalctl`
- Failed service recovery
- Web service validation
- Port verification
- Root cause analysis
- Support documentation
- Customer-facing technical updates

## Scenario Index

| Scenario | Issue | Key Tools | Link |
|---|---|---|---|
| Scenario 001 | Failed Nginx service due to bad configuration | `systemctl`, `journalctl`, `nginx -t` | [View Scenario](scenarios/failed-nginx-bad-config.md) |
| Scenario 002 | Service unavailable due to port conflict | `ss`, `systemctl`, `journalctl` | [View Scenario](scenarios/service-port-conflict.md) |
| Scenario 003 | Service disabled after reboot | `systemctl is-enabled`, `systemctl enable` | [View Scenario](scenarios/service-disabled-after-reboot.md) |

## Investigation Workflow

### 1. Check failed services

```bash
systemctl --failed
```

### 2. Check service status

```bash
sudo systemctl status nginx
```

### 3. Review service logs

```bash
sudo journalctl -u nginx
```

### 4. Validate configuration

```bash
sudo nginx -t
```

For Apache:

```bash
sudo apache2ctl configtest
```

### 5. Restart the service

```bash
sudo systemctl restart nginx
```

### 6. Enable service at boot

```bash
sudo systemctl enable nginx
```

### 7. Confirm listening ports

```bash
sudo ss -tuln | grep :80
```

### 8. Test application access

```bash
curl -I http://localhost
```

## Common Root Causes

- Invalid Nginx or Apache configuration
- Service disabled after reboot
- Port conflict
- Missing dependency
- Incorrect file permissions
- Firewall blocking external access
- Application service not listening on the expected interface

## Verification Checklist

Before closing a service recovery ticket, verify:

- Service is active
- Service is enabled if it should start at boot
- Logs no longer show the same failure
- Service is listening on the expected port
- Local access test succeeds
- External access test succeeds where applicable
- Resolution is documented clearly

## Customer-Facing Update Example

The service availability issue was resolved. The application service had failed due to a configuration issue. The configuration was corrected, the service was restarted, and access was verified.

## Lessons Learned

This lab reinforced the importance of checking service status, logs, configuration validity, listening ports, and application response before closing a support case.

## Portfolio Note

This project is part of my Linux Support Engineer portfolio. It demonstrates practical troubleshooting, documentation, and systems administration skills relevant to Ubuntu/Linux support roles.
