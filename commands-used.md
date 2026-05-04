# Commands Used

This file lists the primary commands used throughout the Ubuntu systemd Service Recovery Lab.

## Check failed services

```bash
systemctl --failed
```

## Check service status

```bash
sudo systemctl status nginx
sudo systemctl status apache2
sudo systemctl status ssh
```

## Review service logs

```bash
sudo journalctl -u nginx
sudo journalctl -u apache2
sudo journalctl -u ssh
```

## Follow logs in real time

```bash
sudo journalctl -u nginx -f
```

## Validate web server configuration

```bash
sudo nginx -t
sudo apache2ctl configtest
```

## Restart services

```bash
sudo systemctl restart nginx
sudo systemctl restart apache2
sudo systemctl restart ssh
```

## Enable services at boot

```bash
sudo systemctl enable nginx
sudo systemctl enable apache2
sudo systemctl enable ssh
```

## Check whether service is enabled

```bash
systemctl is-enabled nginx
systemctl is-enabled apache2
systemctl is-enabled ssh
```

## Confirm listening ports

```bash
sudo ss -tuln
sudo ss -tuln | grep :80
sudo ss -tuln | grep :22
```

## Test local web access

```bash
curl -I http://localhost
curl -v http://localhost
```

## Check firewall status

```bash
sudo ufw status verbose
```
