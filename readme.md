## Set Up NGINX

# Description
In this git repo, we will show how to set up a server to host an index.html file through WSL and remote server and create a cloud firewall

# Usage
- Using **nginx** to create a web server using SSH and HTTP and,
- create a cloud firewall in Digital Oceans

# Setup
- Set up WSL and generate a SSH key in WSL
- Create droplet in Digital Ocean and add the SSH public key in the droplet
- Create regular user in the droplet created and add the key into the user .ssh directory

# Lab
Before following the below instruction, please make sure to complete all setup steps


1. Install NGINX
    1. To make sure all packages up-to-date, run command: sudo apt update && sudo apt upgrade
    2. To install nginx, run command: sudo install nginx
    3. Type "Y" in confirmation questions
    4. Then press Enter to have default package configuration setup
        ![configuration confirm](/images/nginx-package-conf-confirm.png)  

2. Create an index.html or use the index.html from the repo.
    * If using index.html file in the repo, run command: git clone https://github.com/phuongvi1512/2420_week12_Lab.git to download the repo

3. To write nginx server block file, use the sample server-block-file in the repo
    * **Note**: change the domain to your remote server IP address
    ![server block file](/images/nginx-block-server-file.png) 
 


