---
title: Node Server
layout: layout.html
---

# Node Server

The default server for OS.js is Node. Version 4 or above is required (might work on older but not officially supported).

You can install [node supervisor](https://github.com/petruisfan/node-supervisor) and the development (dist-dev) server will automatically reload on change.

## Starting

```bash
# All platforms
$ node osjs run --target=dist      # Start production server
$ node osjs run --target=dist-dev  # Start development server

# Alternative way, NIX
$ ./bin/start-dist.sh  # Start production server
$ ./bin/start-dev.sh   # Start development server (supports watching)

# Alternative way, Windows
$ bin\win-start-dist   # Start production server
$ bin\win-start-dev    # Start development server (supports watching)
```

---

## Running behind a webserver

You can use nginx to run behind a webserver to increase performance and security using a *reverse proxy*.

### nginx

You can run behind nginx using a reverse-proxy:

```
server {
    listen 80;

    server_name osjs.local;

    location / {
        proxy_pass http://localhost:8000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}

```

### apache

You can also run behind Apache using a reverse-proxy:

```bash
$ sudo a2enmod proxy
$ sudo a2enmod proxy_http
```

```
<VirtualHost *:80>
  ServerName osjs.domain.no
  ProxyPass / http://localhost:8000/
</VirtualHost>
```
