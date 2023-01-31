# Project-10
>># LOAD BALANCER SOLUTION WITH NGINX AND SSL/TLS

>>Project Description 
#### This project was a continuation of the previous project with the implementation of a load balancer and a registered domain name registered with SSL certificate, as shown in the project diagram; 

![](PNGs/Nginx%20Diagram.png)

>> Project Steps : 

1. spin up a virtual machine in AWS running Ubuntu version 20.04 LTS 
2. update /etc/hosts with webservers IP4 address from previous project 
3. installing nginx 
- sudo yum install nginx -y

![](PNGs/2.%20Installing%20nginx.png)

4. confirming nginx is running 

![](PNGs/3.%20nginx%20running.png)

5. Editing the hosts file 

![](PNGs/4.%20Editing%20etchosts%20directory.png)

6. Updating nginx config file 

- sudo vi /etc/nginx/nginx.conf

![](PNGs/5.%20Updating%20Config%20file.png)

7. Registering domain with godaddy.com and updating the name server with A-record of Route53 

![](PNGs/1.%20Updating%20Names%20servers%20with%20aws%20.png)

![](PNGs/2.%20Created%20a%20Hosted%20Zone%20AWS.png)

8. Assigning an Elastic IP address with nginx load balancer and associating it to the created domain name so it remains upon reboot

9. updating nginx configuration file with domain 

![](PNGs/5.%20Updating%20Config%20file.png)

10. Ensuring snapd service is running and Installing Certbot

- sudo systemctl status snapd
- sudo snap install --classic certbot

![](PNGs/7.%20Installing%20certbot.png)

11. requesting a certificate 

- sudo ln -s /snap/bin/certbot /usr/bin/certbot
- sudo certbot --nginx

![](PNGs/7.%20Installing%20ssl%20certicate%20to%20domain.png)

12. Site registered with SSL certificate port 443 opened in security group of load balancer 

![](PNGs/8.%20https%20enabled%20site.png)

13. Renewing Certificate using dry-run 
- sudo certbot renew --dry-run

![](PNGs/10.%20renewing%20certicate%20.png)

14. Scheduling a cron job to automatically renew the licence of the certificate 

- crontab -e

- updating the file with the command to renew certificates twice a day 

- * */12 * * *   root /usr/bin/certbot renew > /dev/null 2>&1
