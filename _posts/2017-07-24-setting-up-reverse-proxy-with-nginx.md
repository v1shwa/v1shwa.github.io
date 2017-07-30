---
title: Setting up Reverse Proxy with Nginx
tags: [nginx]
---

Here's a quick snippet to set up Reverse proxy with nginx.

```json
server {
    listen 80;
    server_name www.example.com;
    location /something/ {
        proxy_pass_header Authorization;
        proxy_set_header   Host      $http_host;
        proxy_set_header   X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        
        Access-Control-Allow-Origin: *
        Access-Control-Allow-Methods: POST,GET,PUT,DELETE
        Access-Control-Allow-Headers: Authorization, Lang

        client_max_body_size 0;
        proxy_read_timeout 36000s;

        proxy_pass         http://127.0.0.1:9968/;
    }
    
    location ~ /\. {
         deny all;
    }
}
```
