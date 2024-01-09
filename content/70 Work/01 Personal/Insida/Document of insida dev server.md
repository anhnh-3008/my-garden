#  Server Info

## 1. SSH info
```sh
Host dino_insida_be_dev
  Hostname 13.236.19.173
  User ubuntu
  Port 22
  IdentityFile ~/.ssh/insida_be_dev.pem
```

## 2. Server info
- Server: EC2 instance - t2.small
- OS: ubuntu 22.04
- Node: v18.12.0
- NPM: 8.19.2
- redis-cli 5.0.7
- git ssh
## 3. nginx config

```sh
# /etc/nginx/conf.d/link.api.insida.io.conf

server {
    server_name link.insida.io;
    root /var/www/html;
    error_page 500 502 503 504 /50x.html;
    access_log /var/log/nginx/link.insida.io.access.log;
    error_log /var/log/nginx/link.insida.io.error.log;
    location / {
        index index.php index.html;
        try_files $uri $uri/ =404;
    }
    listen 443 ssl; # managed by Certbot
    ssl_certificate /etc/letsencrypt/live/link.insida.io/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/link.insida.io/privkey.pem; # managed by Certbot
    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot
}

server {
    if ($host = link.insida.io) {
        return 301 https://$host$request_uri;
    } # managed by Certbot
    server_name link.insida.io;
    listen 80;
    return 404; # managed by Certbot
}
```
# Deploy

```
- move to repo: cd /var/www/EarthApp-Backend/
- deploy: git checkout . && git pull && pm2 restart app
- check logs: pm2 logs
```

If nodejs app has the new dependencies, run `npm i` before restart pm2

- Check status of redis-cli: `sudo systemctl status redis`
- If it is stopping, restart it: `sudo systemctl restart redis`