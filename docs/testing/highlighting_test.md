# Highlight test

[https://squidfunk.github.io/mkdocs-material/extensions/admonition/](https://squidfunk.github.io/mkdocs-material/extensions/admonition/)

==HELLO Highlight==

!!! warning
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
    nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
    massa, nec semper lorem quam in massa.

## nginx

```nginx
# make sure that your dns has a cname set for code-server

server {
    listen 443 ssl;
    listen [::]:443 ssl;

    server_name code-server.*;

    include /config/nginx/ssl.conf;

    client_max_body_size 0;

    # enable for ldap auth, fill in ldap details in ldap.conf
    #include /config/nginx/ldap.conf;

    location / {
        # enable the next two lines for http auth
        #auth_basic "Restricted";
        #auth_basic_user_file /config/nginx/.htpasswd;

        # enable the next two lines for ldap auth
        #auth_request /auth;
        #error_page 401 =200 /login;

        include /config/nginx/proxy.conf;
        resolver 127.0.0.11 valid=30s;
        set $upstream_code_server code-server;
        proxy_pass http://$upstream_code_server:8443;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection upgrade;
    }
}
```

## python

```python
print("Unraid rulez")
```

## bash

```bash
#!/bin/bash
echo "Hello world!"
```
