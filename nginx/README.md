
# nginx reverse proxy

More details needed here. Most reverse proxy configurations are similar to this:

```
/etc/nginx/sites-enabled/syncthing.conf

server {
    listen 80;
    server_name  syncthing.somewhere.io;
    location / { return 301 https://$host$request_uri; }
}
server {
    listen 443;
    server_name  syncthing.somewhere.io;
    location / {
        proxy_pass https://192.168.20.100:8384;
    }
}
```
