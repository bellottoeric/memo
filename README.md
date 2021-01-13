sudo nano /etc/nginx/sites-available/default

server {
    listen 80 default_server;
    server_name domain domain.com www.domain.com;
    location / {
        proxy_pass http://127.0.0.1:3000;
    }
}
server {
    listen 80;
    server_name dev.domain dev.domain.com www.dev.domain.com;
    location / {
        proxy_pass http://127.0.0.1:3001;
    }
}

sudo apt-get install certbot python3-certbot-nginx

sudo certbot --nginx -d my.domain.com

sudo ufw allow 2000/tcp
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp


sudo systemctl restart nginx
sudo systemctl restart sshd



sudo nano /etc/fail2ban/jail.d/defaults-debian.conf

[sshd]
enabled = true
port = 2000
logpath  = /var/log/fail2ban.log
banaction = %(banaction_allports)s
bantime  = 1w
findtime = 1d
