# Scenario 002: Service Unavailable Due to Port Conflict

## Reported Issue

A user reports that a web service is unavailable after a new service was installed on the server.

## Impact

The application cannot bind to the required port, so users cannot access the service.

## Environment

- OS: Ubuntu Server
- Service: Nginx or Apache
- Tools: `systemctl`, `journalctl`, `ss`, `curl`

## Investigation Steps

### 1. Check service status

```bash
sudo systemctl status nginx
```

The service fails to start.

### 2. Review service logs

```bash
sudo journalctl -u nginx
```

Logs indicate the service cannot bind to the expected port.

### 3. Check listening ports

```bash
sudo ss -tuln
```

Another process is already listening on port 80.

### 4. Identify conflicting process

```bash
sudo ss -tulnp | grep :80
```

### 5. Stop or reconfigure the conflicting service

Depending on the business need, the conflicting service was stopped, disabled, or moved to another port.

```bash
sudo systemctl stop conflicting-service
```

### 6. Restart the intended service

```bash
sudo systemctl restart nginx
```

### 7. Verify port binding

```bash
sudo ss -tuln | grep :80
```

### 8. Test service response

```bash
curl -I http://localhost
```

## Commands Used

```bash
sudo systemctl status nginx
sudo journalctl -u nginx
sudo ss -tuln
sudo ss -tulnp | grep :80
sudo systemctl stop conflicting-service
sudo systemctl restart nginx
sudo ss -tuln | grep :80
curl -I http://localhost
```

## Root Cause

The web service could not start because another process was already using the required port.

## Resolution

The conflicting service was stopped or reconfigured, and the intended web service was restarted successfully.

## Verification

The correct service was confirmed listening on port 80 and returned a successful response with `curl`.

## Customer-Facing Update

The service outage was resolved. The application could not start because another process was already using the required port. The conflict was corrected and service availability was verified.

## Lessons Learned

Port conflicts can prevent services from starting even when configuration files are valid. Always check listening ports when a service fails to bind.
