# Scenario 001: Failed Nginx Service Due to Bad Configuration

## Reported Issue

A user reports that a web application is unavailable. Attempts to access the site return a connection error.

## Impact

Users cannot access the hosted web application.

## Environment

- OS: Ubuntu Server
- Service: Nginx
- Tools: `systemctl`, `journalctl`, `nginx -t`, `ss`, `curl`

## Investigation Steps

### 1. Check Nginx service status

```bash
sudo systemctl status nginx
```

The service shows as failed.

### 2. Review Nginx logs

```bash
sudo journalctl -u nginx
```

The logs show that Nginx failed during startup.

### 3. Validate Nginx configuration

```bash
sudo nginx -t
```

The configuration test reports a syntax error in an Nginx config file.

### 4. Correct the configuration

The invalid directive or syntax issue was corrected in the affected configuration file.

### 5. Restart Nginx

```bash
sudo systemctl restart nginx
```

### 6. Confirm service status

```bash
sudo systemctl status nginx
```

### 7. Confirm port 80 is listening

```bash
sudo ss -tuln | grep :80
```

### 8. Test local access

```bash
curl -I http://localhost
```

## Commands Used

```bash
sudo systemctl status nginx
sudo journalctl -u nginx
sudo nginx -t
sudo systemctl restart nginx
sudo ss -tuln | grep :80
curl -I http://localhost
```

## Root Cause

Nginx failed to start because of a syntax error in the server configuration file.

## Resolution

The configuration error was corrected, the configuration was validated with `nginx -t`, and Nginx was restarted successfully.

## Verification

Nginx was confirmed active with `systemctl`, listening on port 80 with `ss`, and responding locally with `curl`.

## Customer-Facing Update

The website availability issue was resolved. The web service failed because of a configuration syntax error. The configuration was corrected, the service was restarted, and access was verified.

## Lessons Learned

When a service fails to start, validate configuration files before repeatedly restarting the service. Logs and config-test tools often identify the exact issue.
