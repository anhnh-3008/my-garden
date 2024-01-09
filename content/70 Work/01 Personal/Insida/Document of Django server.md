# I. Tạo instance EC2
- Create Instance, OS Ubuntu 22.04.
- Create ElasticIP and link to the ec2 instance.
- Config Security Group, listen port 22 for ssh, 80 for http and 443 for https.

> [!info] Info connect server
> ```
> Host dino_django_dev
> 	Hostname 3.105.32.43
> 	User ubuntu
> 	Port 22
> 	IdentityFile ~/.ssh/ssh-key-file
> ```

# II. Setup Django project
### 1. Clone repo
- Download Python
- Clone repo: `git clone git@github.com:JuJulius77/Insida_Rec_Engine.git`
- Move repo: `cd Insida_Rec_Engine`

### 2. Setup enviroment
- Create env python: `python3 -m venv devenv`
- Activate: `source devenv/bin/activate`
- Add ENV to `.env` file:
	- DJANGO_SECRET_KEY
	- DEBUG
	- DJANGO_ALLOWED_HOSTS
	- MYSQL_USER
	- MYSQL_DATABASE
	- MYSQL_ROOT_PASSWORD
	- MYSQL_PASSWORD

### 3. Install Lib and dependencies
- `python3 install -r requirements.txt`

### 4. Install Mysql
- google 😁
### 5. Migrate DB
- `python manage.py migrate`

# III. Setup nginx + gunicorn
### 1. Install nginx
- `sudo apt-get install nginx`
- If face to the missing permission error:
	- `sudo chmod a+w /var/log/nginx/*.log`
	- `sudo chmod a+w /var/`
	- `sudo chmod a+w /var/run`

### 2. Install gunicorn
- `pip3 install gunicorn`
- Install supervisor to run process on background.
	- `sudo apt-get install supervisor`

### 3. Setup gunicorn
- Create file: `sudo touch /etc/supervisor/conf.d/gunicorn.conf`
- Settings gunicorn: `sudo vim /etc/supervisor/conf.d/gunicorn.conf`

```conf
program:gunicorn]

directory=/home/ubuntu/Insida_Rec_Engine

command=/home/ubuntu/env/bin/gunicorn --workers 3 --bind unix:/home/ubuntu/Insida_Rec_Engine/app.sock ranking_social.wsgi:application

autostart=true

autorestart=true

stderr_logfile=/var/log/gunicorn/gunicorn.err.log

stdout_logfile=/var/log/gunicorn/gunicorn.out.log

[group:guni]
programs:gunicorn
```

- Add log: `sudo mkdir /var/log/gunicorn`
- Apply log: `sudo supervisorctl reread`
- Add process server: `sudo supervisorctl update`
	- Check status sercer: `sudo supervisorctl status`

### 4. Setup nginx
- Create file: `sudo touch /etc/nginx/sites-availables/django.conf`
- Settings nginx: `sudo vim /etc/nginx/sites-availables/django.conf`

```conf
server{
	listen 80;
	server_name 3.105.32.43;
	location / {
		include proxy_params;
		proxy_pass http://unix:/home/ubuntu/Insida_Rec_Engine/app.sock;
	}
}
```

- Link: `sudo ln django.conf /etc/nginx/sites-enabled`
- Restart nginx to apply changes: `sudo service nginx restart`

> [!note] Note
> If change django server, git pull the newest code and restart: `sudo supervisorctl restart guni:gunicorn`


## 5. Setup SSL
- Use certbot.
- Install `sudo apt-get install certbot`
- Stop nginx: `sudo systemctl stop nginx`
- Gene ssl for domain: `sudo certbot certonly --standalone -d rcm.insidaapp.com`
> Gene cert save in here:
> - ssl_certificate /etc/letsencrypt/live/rcm.insidaapp.com/fullchain.pem;
 >- ssl_certificate_key /etc/letsencrypt/live/rcm.insidaapp.com/privkey.pem;
 
 - Config nginx:
 
```
server {
       listen 443 ssl;
       server_name rcm.insidaapp.com;

       ssl_certificate /etc/letsencrypt/live/rcm.insidaapp.com/fullchain.pem;
       ssl_certificate_key /etc/letsencrypt/live/rcm.insidaapp.com/privkey.pem;

       location / {
            include proxy_params;
            proxy_pass http://unix:/home/ubuntu/Insida_Rec_Engine/app.sock;
       }
}
```

- Add allow host to .env.
- Restart nginx and gunicorn is done!

# When repo has updated
- cd to folder repo: `cd Insida_Rec_Engine`
- `git pull`
- If has the new migration, run: `python3 manage.py migrate`(remmember run `source devenv/bin/activate` before migrate)
- Restart server: `restart server`. This is the alias of the command: `sudo supervisorctl restart guni:gunicorn`

# Some aliases
- Restart Nginx: `restart nginx`. This is the alias of the command: `sudo service nginx restart`

