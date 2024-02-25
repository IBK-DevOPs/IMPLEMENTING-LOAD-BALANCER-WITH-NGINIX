# IMPLEMENTING-LOAD-BALANCER-WITH-NGINIX

## Introduction to load balancer and Nginix

### 1.	What is Nginix
### 2.	Introduction to Nginix
### 3.	Importance of Nginix as load balancer
### 4.	Targeted Audience
### 5.	Prerequisite
### 6.	Goal to be accomplished 

## What is Nginix?
### Nginx, pronounced like “engine-ex,” is a versatile open-source web server that has evolved beyond its initial role. 

## Introduction to Nginix
### It started out as a web server designed for maximum performance and stability. In addition to its HTTP server capabilities, NGINX can also function as a proxy server for email (IMAP, POP3, and SMTP) and a reverse proxy and load balancer for HTTP, TCP, and UDP servers.

## Importance of nginix  (Here’s what Nginix can do)
### 1.Web Server:
#### Nginx started as a high-performance web server.
#### It serves static files, handles requests, and manages connections efficiently.
#### Reverse Proxy:
#### Nginx acts as a reverse proxy, forwarding requests from clients to backend servers (like application servers or other web servers).
#### It balances the load across multiple servers, improving performance and reliability.
### 2. HTTP Cache:
####	Nginx can cache responses, reducing the load on backend servers.
####	It serves cached content directly to clients, enhancing speed.
#### 3.Load Balancer:
#### 4.As a load balancer, Nginx distributes incoming requests across multiple servers.
#### 4.It ensures even resource utilization and fault tolerance.
#### 4. TLS/SSL Termination:
### Nginx handles SSL/TLS encryption for secure communication.
#### It offloads the encryption work from backend servers.
#### 5.	Filters and Scripting:
#### Nginx supports filters like gzip, byte ranges, and image transformation.
#### It can execute scripts using embedded Perl or the njs scripting language.
#### 6.Mail Proxy Server:
#### Nginx can act as a mail proxy server, redirecting requests to IMAP or POP3 servers.
#### It handles user authentication and SSL support.
#### TCP/UDP Proxy Server:
#### Nginx is not limited to HTTP; it can also proxy generic TCP and UDP traffic.
#### It provides load balancing and access control for these protocols.

### Targeted Audience
#### The target audience is web administrators who would like to learn the finer nuances of Nginx, or map their existing skillset from IIS or Apache.
#### Web developers
#### System administrators: 
#### DevOps engineers: 
#### Cloudflare

### Nginx Prerequisites

#### Before you install and start using Nginx, it’s helpful to have the following knowledge and skills.
#### Basic knowledge of networking and web servers: Familiarity with networking concepts and web server technology will help you understand how Nginx works and how to configure it for your specific use case.
#### Familiarity with command line/terminal: Many of the tasks related to installing and managing Nginx will require you to use the command line or terminal, so it’s important to feel comfortable navigating and executing commands in these environments.

### Goals to be accomplished
#### Learner will discover how to distribute traffic efficiently across multiple server, Optimize performance, and ensure high availability for the web application

### In conclusion, Nginx’s high performance, scalability, and flexibility have made it a Favorite among developers and system administrators. It powers major websites and services worldwide.

### Setting up load balancer

#### We are going to be provisioning 2 EC2 inst![alt text](<Images/Free  tier and pem key.png>)ances running Ububtu 22.04

![alt text](<Images/create instance.png>)


![alt text](<Images/Free  tier and pem key.png>)


![alt text](<Images/apache 1 instance detail.png>)


![alt text](<Images/add outbound security port 80 
for Nginix.png>)


![alt text](<Images/connect apache 1 to terminal via ssh.png>)


#### Name it apache server 1 and 2 

#### Connect to terminal via ssh 

![alt text](<Images/EC2  apache 1 ID.png>)

![alt text](<Images/EC2 apache 2 ID.png>)

![alt text](<Images/copy ssh command.png>)


#### Install apache 1 on a terminal with below code

![alt text](<Images/installing apache on server 1.png>)

#### `sudo apt update -y &&  sudo apt install apache2 -y`

#### verify apache 1 is running very well with below code.

![alt text](<Images/systemctl show that apche 1 install very well.png>)

#### `sudo systemctl status apache2`

#### add a new listen directive for port 8000, press I, to switch to insert mode.

![alt text](<Images/add listen directive 8000.png>)


#### add a new listen directive for port 8000, press I, to switch to insert mode

![alt text](<Images/add listen directive 8000.png>)

#### Edit and press escape follow by wq! Then enter
#### Use below code

#### `sudo vi /etc/apache2/ports.conf`

![alt text](<Images/edit file html with public IP.png>)

#### `Open the file/etc/ apache2/sites-available/000-default.conf`


#### Change port 80 on virtual host to 8000

#### `sudo vi /etc/apache2/sites-available/000-default.conf`

![alt text](<Images/virtual host edit 80 to 8000.png>)

#### Save and escape, them press wq! And enter

#### Restart apache with below code

###![alt text](<Images/systemctl show that apche 1 install very well.png>)# `sudo systemctl restart apache2`

#### Create a new  index html file with below code
` mkdir index html`

#### `sudo vi index.html
![alt text](<Images/edit file html with public IP.png>)


#### press I, edit with public IP 

#### press escape, press  wq! Enter

#### Overriding the default htmlfile of apache webserver 

#### Replace the default html file with new html file
#### Using below command

#### `sudo cp -f ./index.html /var/www/html/index.html`

#### Restart the web server to load new configuration
#### With below code 

#### `sudo systemctl restart apache2`

#### ubuntu@ip-172-31-42-254:~$ grep 8000 /etc/apache2/apache2.conf
#### ubuntu@ip-172-31-42-254:~$ grep listen /etc/apache2/apache2.conf
# supposed to determine listening ports for incoming connections which can be
# Include list of ports to listen on
#### ubuntu@ip-172-31-42-254:~$ exit

#### run grep 8000
![alt text](<Images/grep 8000.png>)

#### run grep etc 8000 apache.  

![alt text](<Images/grep etc 8000 apache.png>)

#### Paste public IP of Server 1 and 2 on the web
#### You will see below page

![alt text](<Images/welcome to Ec2 (1).png>)

![alt text](<Images/welcome to EC2 apache 2.png>)

#### Follow the same process for second apache server

![alt text](<Images/EC2 apache 2 ID.png>)

![alt text](<Images/installing apache on server 1.png>)

#### Configure and intall nginix 
![alt text](<Images/add security rule port 80 for Nginix.png>)

![alt text](<Images/add outbound security port 80 for Nginix.png>)

![alt text](<Images/installation of Nginix.png>)

![alt text](<Images/verify Nginix is properly installed.png>)

#### run below code

#### `sudo apt update -y && sudo apt install nginx -y`

#### Add outbound rule with port 80 to install nginix
![alt text](<Images/add outbound security port 80 for Nginix.png>)

#### Verify that Nginix is install with below code
![alt text](<Images/verify Nginix is properly installed.png>)

#### Then verify Nginix with below code

#### `sudo systemctl status nginx`

#### Open Nginix configuration file with below code

#### `sudo vi /etc/nginx/conf.d/loadbalancer.conf`

![alt text](<Images/Edit server 1 &2 and Nginix servers IP.png>)

#### Then put the following, and edit local IP of the server
        
`upstream backend_servers {

            # your are to replace the public IP and Port to that of your webservers
            `server 127.0.0.1:8000; # public IP and port for webserser 1`
            `server 127.0.0.1:8000; # public IP and port for webserver 2`

        }

        server {
            listen 80;
         `   server_name <your load balancer's public IP addres>; # provide your load balancers public IP address`

            location / {
              `  proxy_pass http://backend_servers;`
               ` proxy_set_header Host $host;`
               ` proxy_set_header X-Real-IP $remote_addr;`
                `proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;`
            }`
        }`
    Test Nginix configuration with below code
      sudo nginx -t` 


#### You will see this


#### `ubuntu@ip-172-31-42-127:~$ sudo nginx -t
`nginx: the configuration file /etc/nginx/nginx.`conf syntax is ok`

`nginx: configuration file /etc/nginx/nginx.conf test is successful`
`ubuntu@ip-172-31-42-127:~$`

#### if there is no error, reload or restatrt Nginix with below code.

![alt text](<Images/Test nginix configuration of servers IP.png>)

`sudo systemctl restart nginx`

#### Paste public IP address of Nginix load balance on a web.

#### We will see below page

![alt text](<Images/Welcome to Nginix.png>)





























































