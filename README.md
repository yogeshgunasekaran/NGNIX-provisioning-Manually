# NGNIX-provisioning-Manually
Installation of NGNIX in Ubuntu. Nginx is a front-end web server, used as a load balancer which receives the request from client and send the request to its application servers.
### Log in to root user
```sh
sudo su -
```
### Update OS with latest patches
```sh
apt update
```
```sh
apt upgrade
```
### Install Ngnix
```sh
apt install nginx -y
```
### Create Nginx config file with below content
This Configuration file will re-direct request from ngnix to tomcat servers on port 8080.
```sh
vi /etc/nginx/sites-available/<enter 'project name' here>
```
~~~
upstream <project name> {
server <tomcat server ip>:8080;
}
server {
listen 80;
location / {
proxy_pass http://<project name>;
}
}
~~~
#### <ins> *Note*</ins>  : <br>
> where there are more than 1 application server, just add the application server ip's in the upstream as below, <br>
> upstream ngnixproj { <br>
> server 192.168.24.35:8080; <br>
> server 192.168.24.24:8080; <br>
> server 192.168.24.78:8080; <br>
> server 192.168.24.13:8080; <br>
> } <br>
> server { <br>
> listen 80; <br>
> location / { <br>
> proxy_pass http://ngnixproj; <br>
> } <br>
> } <br>



### Remove default Nginx config file
```sh
rm -rf /etc/nginx/sites-enabled/default
```
### Create link to activate website
```sh
ln -s /etc/nginx/sites-available/<project name> /etc/nginx/sites-enabled/<project name>
```
### Restart Nginx
```sh
systemctl restart nginx
```

