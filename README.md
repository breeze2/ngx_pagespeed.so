# ngx_pagespeed.so
nginx dynamic module ngx_pagespeed.so

In NGINX 1.9.11 onwards a new way of loading modules dynamically has been introduced.
There are some ngx_pagespeed.so, which have been compiled, you can download one and load it dynamically for your nginx.

## About Pagespeed

ngx_pagespeed is an nginx moudle created by Google to help Make the Web Faster by rewriting web pages to reduce latency and bandwidth. More at [pagespeed/ngx_pagespeed](https://github.com/pagespeed/ngx_pagespeed)

## Installation

### git clone

```cmd
$ mkdir ~/tmp
$ cd ~/tmp
$ git clone https://github.com/breeze2/ngx_pagespeed.so.git
$ cd tmp
```

### Copy to 

If your operating system is Ubuntu16.04, and you install nginx with `sudo apt-get install nginx` directly, (maybe you should run `sudo apt-get update && apt-get upgrade nginx` first), run

```cmd
$ sudo mkdir /usr/share/nginx/modules
$ cp ./ubuntu_x86_64/nginx-xenial-1.10.3/ngx_pagespeed.so /usr/share/nginx/modules/
```


If you install nginx with `sudo add-apt-repository ppa:nginx/stable && apt-get update && apt-get install nginx`, (maybe you should run `sudo apt-get update && apt-get upgrade nginx` first), run

```cmd
$ sudo mkdir /usr/share/nginx/modules
$ cp ./ubuntu_x86_64/nginx-stable-1.12.1/ngx_pagespeed.so /usr/share/nginx/modules/
```


### Load Module

edit `/etc/nginx/nginx.conf`, e.g.

```conf
user www-data;
worker_processes auto;
pid /run/nginx.pid;

load_module modules/ngx_pagespeed.so;

events {
        worker_connections 768;
        # multi_accept on;
}

http {
    ...
}
```


### Test 

run `sudo nginx -t`, if you get output as follow, that means it works

```cmd
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```

## Usage

```cmd
$ sudo mkdir /var/cache/ngx_pagespeed -p
$ sudo chown www-data:www-data -R /var/cache/ngx_pagespeed
```

edit `/etc/nginx/sites-enabled/default`, e.g.

```conf
server {
    listen 80;
    
    pagespeed on;
    pagespeed FileCachePath /var/cache/ngx_pagespeed;

    root /var/www/html;
    ...
}

```


## Only For

The ngx_pagespeed.so is only for Ubuntu x86_64. In other environments, maybe it works, you can have a try.

## How to compile your ngx_pagespeed module manually
coming soon...