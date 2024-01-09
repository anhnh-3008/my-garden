# Settings gunicorn
- Path: `/etc/systemd/system/buybuymotors_be.service`

```sh
[Unit]
Description=Gunicorn instance to serve buybuymotors_be
After=network.target

[Service]
User=root
Group=www-data
WorkingDirectory=/var/www/buybuymotors_BE/app
Environment="PATH=/var/www/buybuymotors_BE/devenv/bin"
ExecStart=/var/www/buybuymotors_BE/devenv/bin/gunicorn --workers 3 --bind unix:/var/www/buybuymotors_BE/app.sock wsgi:app --log-file /var/log/buybuymotors_be/server.log --log-level debug

[Install]
WantedBy=multi-user.target
```

# Settings Nginx
- Path: `/etc/nginx/sites-available/buybuymotors_be`

```sh
server {
    server_name pre.buybuymotors.com;

    location / {
        include proxy_params;
        proxy_pass http://unix:/var/www/buybuymotors_BE/app.sock;
    }

    listen 443 ssl; # managed by Certbot
    ssl_certificate /etc/letsencrypt/live/pre.buybuymotors.com/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/pre.buybuymotors.com/privkey.pem; # managed by Certbot
    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot
}

server {
    if ($host = pre.buybuymotors.com) {
        return 301 https://$host$request_uri;
    } # managed by Certbot

    listen 80;
    server_name pre.buybuymotors.com;
    return 404; # managed by Certbot

}
```

# Settings logrotate

```
/var/log/buybuymotors_be/*.log {
    daily                # Rotate logs daily
    size 100M            # Only rotate when the file size exceeds 100MB
    rotate 3             # Keep the 3 most recent logs
    compress             # Compress the log files before rotating
    missingok            # Do not throw an error if the file does not exist
    notifempty           # Do not rotate the file if it is empty
    create 640 root adm  # Create new log files with specified permissions
    postrotate           # Script to run after log rotation
        /bin/systemctl restart buybuymotors_be.service
    endscript
}
```

# Deploy
1. Pull code from git
2. Run command: `server-restart`. This is alias of command: `sudo systemctl restart buybuymotors_be.service`.

# Commands
- Check status of server: `server-status`. This is alias of command: `sudo systemctl status buybuymotors_be.service`.
- Check log of Flask server: `server-logs`. This is alias of `sudo tail -f /var/log/gunicorn/server.log`
- Check log of Flask server: `nginx-restart`. This is alias of `sudo systemctl restart nginx`
- Check log of Flask server: `nginx-status`. This is alias of `sudo systemctl status nginx`
- Check log of Flask server: `nginx-error-logs`. This is alias of `sudo tail -f /var/log/nginx/error.log`
- Check log of Flask server: `nginx-access-logs`. This is alias of `sudo tail -f /var/log/nginx/access.log`