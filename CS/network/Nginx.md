# Nginx deploy static HTML in Ubantu


```bash
sudo apt update
sudo apt install nginx
```



```bash
sudo systemctl start nginx
sudo systemctl enable nginx
```



the path: `/etc/nginx/sites-available/` put the config file(No suffix .conf)

```bash
vim your_domain

server {
    listen 80;
    server_name ip domain1 domain2;

    root /var/www/temp;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

then enable it

```bash
sudo ln -s /etc/nginx/sites-available/your_domain /etc/nginx/sites-enabled/
```

Test the config

```bash
sudo nginx -t
```

If OK, reload:

```bash
sudo systemctl reload nginx
```

