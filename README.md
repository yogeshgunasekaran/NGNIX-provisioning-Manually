# NGNIX-provisioning-Manually
Installation of NGNIX in Ubuntu
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
```sh
vi /etc/nginx/sites-available/<enter project name here>
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
### Remove default Nginx config file
```sh
rm -rf /etc/nginx/sites-enabled/default
```
### Create link to activate website
```sh
ln -s /etc/nginx/sites-available/<project file> /etc/nginx/sites-enabled/<project file>
```
### Restart Nginx
```sh
systemctl restart nginx
```

