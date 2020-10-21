# OVERVIEW

## WEB SERVER APPACHE

Web server are computers which delivers the requested web pages.Every web server has an IP address and a Domain Name. EG:(XAMPP,Apache,NGINX,Tornado,Caddy,Microsoft IIS)

## NGINX

* NGINX is open source software for web serving,reverse proxying,Caching, load balancing ,media streaming and more.Its web server designed for maximum performance and stability
* Nginx can also function us proxy server for email(IMAP,POP3 AND SMTP) and a reverse proxy and Load balancer for HTTP,TCP and UDP servers.

![fundamental](nginx_arch.png)

## BASIC COMMANDS

* Sudo systemctl status nginx
* Sudo systemctl stop nginx
* Sudo systemctl start nginx
* Sudo systemctl reload nginx

server {
    location / {
        root /data/www;
    }

    location /images/ {
        root /data;
    }
}

# INSTALLATIION

## SERVER OVERVIEW

* Created an Instance in EC2 with the enabling PORT 20,80,443
* By using the Public IP of EC2 instance login into machine using SS H command  
  Eg:sudo ssh -i/home/sarath/Downloads/EC2Tutorial.pem ubuntu@52.66.105.255
         
## INSTALLING WITH A PACKAGE MANAGER 

  UBUNTU
* sudo apt-get update -clear
* sudo apt-get install nginx -clear
* ps aux | grep nginx (navigate to browser using IP into Nginx page)
* ls -l /etc/nginx/ (To see conf files in nginx)
* Download the nginx mainline version for nginx.org website.
* wget (paste the link of mainline version) 
* ls -l
* tar -zxvf (paste tar file. eg:nginx -1.13.10.tar.gz)
* ls -l
* cd nginx-(type version as above)
* we need to install a compiler to compile source code
* sudo apt-get install build-essential   -clear (to test ./configure)
* sudo apt-get install libpcre3 libpre3-dev zlib1g zlib1g-dev libssl-dev(pcre library)

## CUSTOM CONFIGURATION COMMAND

* sudo ./configure --sbin-path=/usr/bin/nginx --conf-path=/etc/nginx/nginx.conf --error-log-path=/var/log/nginx/error.log --http-log-path=/var/log/nginx/access.log --with-pcre --pid-path=/var/run/nginx.pid --with-http_ssl_module
* Make
* sudo install make    --ls -l /etc/nginx (to check the conf file exit)
* nginx     --ps aux | grep nginx

## SYSTEMD SERVICE(Managing a better way Nginx)

* ps aux | grep nginx (check nginx is running)
* nginx -h (commands for help version)
* nginx -s stop    ----ps aux | grep nginx
* touch /lib/systemd/system/nginx.service
* sudo nano /lib/systemd/system/nginx.service
* systemctl start nginx
* ps aux | grep nginx
* systemctl stop nginx(load the web page)
* systemctl enable nginx
* reboot   (To login again type ssh command)


# CONFIGURATION

* ls -l  /sites/demo/ ( create a directory)
* Upload three files into it(index.html,style.css,thump.png)
* ls -l /etc/nginx/( file to edit is nginx.conf)
* sudo nano nginx.conf
  ``` events {}
      
      http {
         
         include mime.types;

         server {

           listen 80;
           server_name IP:

           root /sites/demo;
         }
      } ```
* nginx -t
* systemctl reload nginx
* curl -I http://IP/style.css
* Reload the browser

## LOCATION BLOCKS

* Exact match  =uri
* Preferential Prefix match  ^~
* Regex Match   ~*
* Prefix match  uri
  ``` events {}
      
      http {
         
         include mime.types;

         server {

           listen 80;
           server_name IP:

           root /sites/demo;

           location /greet { 
             return 200 'Hello from NGINX "/great" location.';
           }  
         }
      } ```

## VARIABLES

CONFIGURATION VARIABLES- set $var 'something';
NGINX MODULE VARIABLES-$http,$uri,$args

``` 
events {}

http {

  include mime.types;

  server {

    listen 80;
    server_name 167.99.93.26;

    root /sites/demo;

    set $mon 'No';

    # Check if weekend
    if ( $date_local ~ 'Monday' ) {
      set $mon 'Yes';
    }



    location /is_monday {

      return 200 $mon;
    }
  }
 }
  ```
* Sudo systemctl upload nginx
* Reload the browser page  IP/is_monday

## REWRITES AND REDIRECTS

* Rewrite pattern URI
* Return status  URI

 events {}

http {

  include mime.types;

  server {

    listen 80;
    server_name 167.99.93.26;

    root /sites/demo;

    location /logo {

      return 307 /thump.png;
    }
  }
}   

REWRITES

events {}

http {

  include mime.types;

  server {

    listen 80;
    server_name 167.99.93.26;

    root /sites/demo;

    rewrite ^/user/(\w+) /greet/$1 last;
    rewrite ^/greet/john /thumb.png;

    location /greet {

      return 200 "Hello User";
    }

    location = /greet/john {
      return 200 "Hello John";
    }
  }
}
## TRY FILES AND NAMED LOCATION

* events {}

http {

  include mime.types;

  server {

    listen 80;
    server_name 167.99.93.26;

    root /sites/demo;

    try_files /thump.png /greet; or try_files $uri /cat.png /greet;

    location /greet{
      return 200 "Hello user";
    }
  }
}
## LOGGING

* Error log
* Access log

* ls -l /var/log/nginx/
* cd /var/log/nginx/
* echo ''> access.log
* echo ''> error log
* ls -l
* cat access.log

