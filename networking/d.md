# Reverse Proxies

---

1. install nginx

```
sudo apt update
sudo apt install nginx -y
```

2. put available configs under sites-available directory

```
sudo nano /etc/nginx/sites-available/myapp
```

3. edit config for

a. Reverse Proxy

```
server {
    listen 80;

    server_name myapp.com;

    location / {
        proxy_pass http://127.0.0.1:8080;

        # Pass original client info
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

b. Load balancing

```
upstream backend {
    server 127.0.0.1:8080;
    server 127.0.0.1:8081;
}

server {
    listen 80;
    location / {
        proxy_pass http://backend;
    }
}
```

4. Apply config

```
sudo ln -s /etc/nginx/sites-available/myapp /etc/nginx/sites-enabled/myapp
sudo nginx -t # test nginx config
sudo systemctl reload nginx.service
```
