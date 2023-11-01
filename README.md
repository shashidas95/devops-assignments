# assignments-

- start connection VM with mobaxterm
- from vm start
- ubuntu-server login ubuntu-server
- password ***
- open mobaxterm -> session -> remote host ip address -> check the box->ubuntu-server->ok
  

1. how to find a ip of a domain 
```
ping shashikanta.com
or
nslookup shashikanta.com
```
2. how to find a ip of router assigned by isp
```
ifconfig
or
ip route | grep default

```
2. how to find the private ip of a host machine
```
ip a
```
2. how to find the private ip of a host machine
```
netstat -tuln
explaination of commands

netstat -tuln, the command will provide you with a list of open TCP and UDP ports on your system, specifically showing the listening ports, and it will display them as numeric IP addresses and port numbers, making it easier to identify and work with the network connections and services on your computer.
```
5. to open port 3306 (MySQL) and port 80 (HTTP) on a VM running Ubuntu with ufw:
```
sudo ufw allow 3306/tcp
sudo ufw allow 80/tcp
sudo ufw reload
```
if Firewall not enabled (skipping reload)
```
sudo ufw enable
```
if Firewall is active and enabled on system startup
```
sudo ufw status
```

 
7. To install the Nginx web server on a virtual machine (VM) and access the welcome page, you can follow these general steps.

- First, access your VM via SSH. Use the following command, replacing your-username and your-vm-ip with your actual username and VM's IP address:
```
ssh your-username@your-vm-ip
```
Update Package Repository:
```
sudo apt update
```
Install Nginx:
```
sudo apt install nginx
```
Start and Enable Nginx:
```
sudo systemctl start nginx
sudo systemctl enable nginx
```
If a firewall is running on your VM, you may need to allow HTTP traffic (port 80) through the firewall. The command to do this depends on your firewall tool (e.g., ufw, firewalld, iptables).
on Ubuntu with UFW (Uncomplicated Firewall), you can allow HTTP traffic with:
```
sudo ufw allow 3306/tcp
sudo ufw allow 80/tcp
sudo ufw reload
sudo ufw enable
sudo ufw status
```
Access the Welcome Page:
Open a web browser and enter your VM's IP address in the address bar. You should see the Nginx welcome page. The URL will be http://your-vm-ip.
If you're not sure about the VM's IP address, you can find it by running:
```
ip a
```

If you want to serve your own web content or customize Nginx further, you can edit the configuration files located in the /etc/nginx directory. 
The default web root directory is usually /var/www/html.

6. To download a file or install a package from the terminal in a Linux-based operating system Using APT (Advanced Package Tool) 
```
sudo apt update
sudo apt install package-name
```
To download a file:
```
wget https://example.com/file-url
example
wget www.shashikanta.com
```
8. You can retrieve web data from the terminal in Linux using several command-line tools.
Two common tools for this purpose are curl and wget. Here's how to use them to fetch web data:

```
curl https://example.com
or
wget https://example.com
```
You can also save the web data to a file using the -o option:

```
curl -o output.html https://example.com
or
wget -O output.html https://example.com
```

9. Creating a MySQL database server in a virtual machine (VM) and accessing it from your local machine involves several steps.

- Install MySQL Server:

- SSH into your VM : First, access your VM via SSH. Use the following command, replacing your-username and your-vm-ip with your actual username and VM's IP address:
```
ssh your-username@your-vm-ip
```
- install the MySQL server:
 ```
sudo apt update
sudo apt install mysql-server
 ```
- Configure MySQL:
```
sudo mysql_secure_installation

```
- Allow External Access: By default, MySQL may only listen for connections from the localhost. To allow external access, you need to modify the MySQL configuration. Edit the MySQL configuration file:
```
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf

```
- Look for the bind-address directive and change it to the VM's IP address or 0.0.0.0 to allow connections from any IP (not recommended for production):
```
bind-address = 0.0.0.0

```
Save the file and exit the text editor.

- Create a Database and User:

- Access the MySQL shell:
```
mysql -u root -p

```
- Create a database and user with appropriate privileges:
```
CREATE DATABASE your_database_name;
CREATE USER 'your_username'@'%' IDENTIFIED BY 'your_password';
GRANT ALL PRIVILEGES ON your_database_name.* TO 'your_username'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;

```
Replace your_database_name, your_username, and your_password with your preferred values.

- Allow MySQL Port Through Firewall: If a firewall is enabled on your VM, allow incoming connections to MySQL port (default is 3306):

For Ubuntu with UFW:
```
sudo ufw allow 3306/tcp

```
- Access MySQL Server from Your Local Machine: On  local machine, use a MySQL client (e.g., MySQL Workbench, phpMyAdmin, or the command-line mysql tool) to connect to the MySQL server using the VM's public IP address. Use the username and password you created in step 4.

Example using the command-line MySQL client:
```
mysql -h vm_ip_address -u your_username -p

```
You'll be prompted for the password you set in step 4.
Now, you should be able to access the MySQL database server in your VM from your local machine or host using the VM's public IP address. Make sure to consider security best practices and, if needed, configure firewall rules, security groups, or network settings to allow the traffic between your local machine and the VM.


20. how to Reset the MySQL Root Password:
```
sudo systemctl stop mysql


```
run MySQL in safe mode with the --skip-grant-tables option. This allows you to access MySQL without authentication:
```
sudo mysqld_safe --skip-grant-tables --skip-networking &
```

if "Directory '/var/run/mysqld' for UNIX socket file doesn't exist": This message indicates that the directory '/var/run/mysqld,' where MySQL's UNIX socket file is expected to be located, does not exist. You can create this directory if it doesn't already exist:
```
sudo mkdir /var/run/mysqld

```
After creating the directory, you can start the MySQL server in safe mode again:
```
sudo mysqld_safe --skip-grant-tables --skip-networking &


```
Then, access MySQL without a password:
```
mysql -u root

```
Now, you can change the root password. Replace new_password with your desired password:
```
FLUSH PRIVILEGES;
ALTER USER 'root'@'localhost' IDENTIFIED BY 'new_password';

```
After setting the password, exit MySQL and restart the MySQL service:
```
exit
sudo service mysql start 
```
