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

- systemd service troubleshooting
- Log analysis with `journalctl`
- Failed service recovery
- Web service validation
- Port verification
- Root cause analysis
- Support documentation

## Investigation Workflow

### 1. Check failed services

```bash
systemctl --failed
