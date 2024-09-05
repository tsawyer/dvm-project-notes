## Nginx Reverse Proxy

This is my `/etc/nginx/sites-available/reverse-proxy.conf` configuration file for DVMHost REST.

```
server {
    listen 8085;
    server_name awp25.net;

    location / {
        auth_basic "Restricted Access";
        auth_basic_user_file /etc/nginx/.htpasswd;

        proxy_pass http://127.0.0.1:8180;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header X-Forwarded-Host $host;
	proxy_set_header X-Forwarded-Prefix /;
    }
}
```
