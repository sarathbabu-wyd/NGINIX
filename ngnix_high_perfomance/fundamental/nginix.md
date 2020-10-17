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
* ps aux | grep nginx (navigate to browser using nginx page)
* ls -l /etc/nginx/

  CENTOS
*   
