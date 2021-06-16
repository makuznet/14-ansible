# Ansible roles
> This repo is an example of rolling out NGINX and PHP on different servers. 

## Usage
Edit document root dir, change user name, edit nginx.conf and www.conf files before running the command that roll this all out.  
To roll out run:
```bash
terraform init
terraform apply --auto-approve
```
### Edit document root
Go to roles > http > tasks > main.yml.  
Find `conveying files via template` task.   
Find `/opt/nginx/ansible/index.php` and change the path.  
Go to roles > http > templates > nginx.conf.j2 template.  
Find `root /opt/nginx/ansible;` and change the path.

### Change user name
Go to roles > users > tasks > main.yml > create users > loop and change a user name.  

### Edit nginx.conf
Go to roles > http > templates > nginx.conf.j2 and change its content.  
Pay attention to instructions:  
Your PHP server IP address:  
```bash
fastcgi_pass 192.168.9.20:9000;
```
Your PHP server root document path:  
```bash
fastcgi_param SCRIPT_FILENAME /opt/nginx/ansible$fastcgi_script_name;
```
### Edit www.conf of PHP server
Go to files > www.conf  
Change next lines:  
What interface your PHP server will listen:  
```bash
listen = 192.168.9.20:9000
```
What NGINX IP address connections your PHP server will accept:  
```bash
listen.allowed_clients = 192.168.9.10
```
### Change index.php with other content
Use copy task or shell task to copy or clone your project to your document root directory.  

## Extra
Manual php-fpm restart, Debian:  
```bash
sudo service php7.3-fpm restart
```

## Installation
You should have Terraform and Ansible on your host to roll that out.
You also should have Yandex.Cloud account and your credentials listed in main.auto.tfvars.sample.

## Acknowledgments
This repo was inspired by [skillfactory.ru](https://skillfactory.ru/devops#syllabus) team

## See also
- [Nginx to serve php files from a different server](https://stackoverflow.com/questions/44706951/nginx-to-serve-php-files-from-a-different-server)  
- [How do you restart php-fpm?](https://serverfault.com/questions/189940/how-do-you-restart-php-fpm)  

## License
Follow all involved parties licenses terms and conditions.