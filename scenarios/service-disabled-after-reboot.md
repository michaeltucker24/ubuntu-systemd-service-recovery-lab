# Scenario 003: Service Disabled After Reboot

## Reported Issue

A user reports that an application was working previously, but it became unavailable after the server rebooted.

## Impact

The service does not start automatically after reboot, causing application downtime.

## Environment

- OS: Ubuntu Server
- Service: Nginx, Apache, SSH, or custom application service
- Tools: `systemctl`, `journalctl`, `ss`, `curl`

## Investigation Steps

### 1. Check service status

```bash
sudo systemctl status nginx
```

The service is inactive after reboot.

### 2. Check whether the service is enabled

```bash
systemctl is-enabled nginx
```

The service is disabled.

### 3. Review recent service logs

```bash
sudo journalctl -u nginx
```

Logs do not show a startup attempt after reboot.

### 4. Start the service manually

```bash
sudo systemctl start nginx
```

### 5. Enable the service at boot

```bash
sudo systemctl enable nginx
```

### 6. Confirm service status

```bash
sudo systemctl status nginx
```

### 7. Confirm service is enabled

```bash
systemctl is-enabled nginx
```

### 8. Test application access

```bash
curl -I http://localhost
```

## Commands Used

```bash
sudo systemctl status nginx
systemctl is-enabled nginx
sudo journalctl -u nginx
sudo systemctl start nginx
sudo systemctl enable nginx
sudo systemctl status nginx
curl -I http://localhost
```

## Root Cause

The service was installed and working, but it was not enabled to start automatically after reboot.

## Resolution

The service was started manually and enabled to start automatically at boot.

## Verification

The service was confirmed active, enabled, and responding to local access tests.

## Customer-Facing Update

The application became unavailable after reboot because the service was not enabled to start automatically. The service was started, enabled at boot, and verified successfully.

## Lessons Learned

A service can work correctly during manual testing but still fail after reboot if it is not enabled. Always confirm both service status and enablement state.
