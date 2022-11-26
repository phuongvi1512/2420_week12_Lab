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


1. Install NGINX on your Server
    1. To make sure all packages up-to-date, run command: sudo apt update && sudo apt upgrade
    2. To install nginx, run command: sudo install nginx
    3. Type "Y" in confirmation questions
    4. Then press Enter to have default package configuration setup
        ![configuration confirm](/images/nginx-package-conf-confirm.png)  

2. Create an index.html or use the index.html from the repo.
    * If using index.html file in the repo, run command: git clone https://github.com/phuongvi1512/2420_week12_Lab.git to download the repo

3. To write a nginx server block file, use the sample server-block-file in the repo
    **Note**: change the domain to your remote server IP address from DigitalOCean
    ![server block file](/images/nginx-block-server-file.png) 

4. To upload the file from your local host (wsl) to server, use command sftp
    1. To connect to remote server, run command: sftp username@remote-server-IP-address
    2. To upload folder you downloaded from the repo, in sftp, run command: put -r folder-name
    3. Move files to approriate directories:
        * Move index.html file into /var/www/IP-address/html/ dir
            > command: sudo mv index.html /var/www/IP-address/html/
            
            **Note**: You may need to create folder /var/www/IP-address/hmtl and change ownership and permission
            > sudo mkdir -p /var/www/IP-address/html
            > sudo chown -R $USER:$USER /var/www/IP-address
            > sudo chmod -R 755 /var/www/IP-address
            ![command to make www dir](/images/command-setup-server-block.png)

        * To create directive for server block file, move server-block-file to /etc/nginx/sites-available and rename the file to the domain or IP address
            > command: sudo mv server-block-file /etc/nginx/sites/available/IP-address

        * Create symbolic link using command: 
            > command: sudo ln -s /etc/nginx/sites-available/IP-address /etc/nginx/sites-enabled

        * Test the configuration using command
            > sudo nginx -t
            ![command to test configuration](/images/nginx-check-conf-file.png)

5. To restart nginx service, use command: sudo systemctl restart nginx
    To check if the command works, run command: systemctl status nginx. It should show active and running
    

6. To check if the server IP address is served, in your choice's web browser (google chrome, firefox, etc), type: http://IP-address and press Enter

7. Set up cloud firewall in Digital Ocean
    1. Sign in and go to your projects page, in left drop down menu, click on **Networking** and then choose **Firewall** and click **Create Firewall**
    ![set up firewall 1](/images/firewall-create.png)



    2. In **Name** section, add the name of your firewall then add inbound rules
    ![set up firewall 1](/images/firewall-add.png)
    * Note: in the below image, since only **SSH** and **HTTP** are added in inbound rules, the remote server is only connected through **SSH** and **HTTP** protocols
    * If you want the remote server to be connected through certain protocols, edit the inbound rules

    ![set up firewall 1](/images/firewall-name-inbound-rules.png)




    3. In **Apply to Droplets**, add <ins>tag</ins>
    * Note: The <ins>tag</ins> must be matching with the tag of the droplets you want to put firewall
    ![set up firewall 1](/images/firewall-add-tag.png)
    ![droplet tag](/images/droplet-create.png)




    4. Click **Created**, the firewall will be created. 
    ![set up firewall 1](/images/firewall-created.png)
    
 
8. Check if the server IP address works after activation cloud firewall


