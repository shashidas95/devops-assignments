# how to connect with mobaxterm with vm
- start connection VM with mobaxterm
- from vm start
- ubuntu-server login ubuntu-server
- password ***
- open mobaxterm -> session -> remote host ip address -> check the box->ubuntu-server->ok
# assignments-on networking

- 1. how to find ip of a domain?
- 2. how to find router ip assigned by the ISP?
- 3. how to find private ip of host machine?
- 4. how to change private ip of a ubuntu machine?
- 5. check ports open in the current system?
- 6. enable port 80 and 3306 in vm
- 7. download any file or software using terminal
- 8. get web data response from terminal
- 9. install nginx webserver in the vm and access the welcome nginx  page from web browser
- 10. create a mysql database server in vm and access it from host machine
- 11. replace default nginx welcome page with an index.html page containing your name and access it from web browser
- 12. display the same index.html file in "your_name.com" by utilizing hostname of vm and host machine


Submission Guideline: Submit commands for the first four questions(for safekeeping purposes we don't recommend you to reavel your IP) and for the rest submit commands and corresponding screenshots. Create .sh files for each task. Create a documentation.pdf explaining each task with related screenshots.
If you are unable turn in your task, please submit it in the comment section. 

Submission Deadline: 16th October, 2023, Monday 11:59 PM

# commands for assignment on networking
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
3. how to find the private ip of a host machine
```
ip a
```
- 4. how to change private ip of a ubuntu machine?
Identify the Network Interface:
```
ifconfig
# or
ip addr
```
Backup Network Configuration:
```
sudo cp /etc/netplan/01-netcfg.yaml /etc/netplan/01-netcfg.yaml.bak
```
Edit Network Configuration:
```
sudo nano /etc/netplan/01-netcfg.yaml
```
Change the IP Address:
```
addresses:
  - 192.168.0.104/24
```
Apply the Changes:
```
sudo netplan apply
```
Verify the New IP Address:
```
ifconfig
# or
ip addr
```
5. check ports open in the current system?
```
netstat -tuln
explaination of commands

netstat -tuln, the command will provide you with a list of open TCP and UDP ports on your system, specifically showing the listening ports, and it will display them as numeric IP addresses and port numbers, making it easier to identify and work with the network connections and services on your computer.
or
ss -tuln
or
sudo apt install nmap
sudo nmap -p- localhost


Please note that the nmap command may require superuser privileges to scan all ports.
```
6. enable port 3306 (MySQL) and port 80 (HTTP) on a VM running Ubuntu with ufw:
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

 
9. To install the Nginx web server on a virtual machine (VM) and access the welcome page, you can follow these general steps.

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

7. To download a file or install a package from the terminal in a Linux-based operating system Using APT (Advanced Package Tool) 
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
You can retrieve web data from the terminal in Linux using several command-line tools.
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
ssh your-username@your-vm-ip  **note optional**
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
sudo mysql 

```
- Create a database and user with appropriate privileges: for accessing from localhost
```
CREATE DATABASE your_database_name;
CREATE USER 'your_username'@'localhost' IDENTIFIED BY 'your_password';
GRANT ALL PRIVILEGES ON your_database_name.* TO 'your_username'@'localhost' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```
- Create a database and user with appropriate privileges: for accessing from vm
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
- 11. replace default nginx welcome page with an index.html page containing your name and access it from web browser
Create a Custom index.html File:
```
nano /var/www/html/index.html
```
```

Replace /var/www/html with the appropriate web server root directory path if it's different on your system.
```
Add your content to the index.html file. For example:
```
<!DOCTYPE html>
<html>
<head>
    <title>My Personal Page</title>
</head>
<body>
    <h1>Hello, I am [Your Name]</h1>
</body>
</html>

```
Save the file and exit the text editor.

Restart Nginx:

After creating the custom index.html file, you need to restart the Nginx web server to apply the changes:
```
sudo systemctl restart nginx
Access the Custom Page from a Web Browser:
```
Open your web browser and enter the IP address or domain name of your server. You should see your custom page with your name displayed.

For example, if your server's IP address is 192.168.0.103, you can access it by entering the following URL in your web browser's address bar:
```
http://192.168.0.103
```
You should see the custom index.html page you created with your name displayed on the web page.

- 12. display the same index.html file in "your_name.com" by utilizing hostname of vm and host machine
 
To display the same `index.html` file in "your_name.com" by utilizing the hostname of your VM and host machine, you'll need to make changes to the hosts file on your host machine. Here are the steps to achieve this:

Edit the Hosts File on Your Host Machine:
On your host machine, you need to edit the hosts file to map "your_name.com" to the IP address of your VM. This allows your host machine to resolve "your_name.com" to the correct IP address. You'll typically need administrative privileges to edit the hosts file.

   - On Windows:
     Open Notepad or your preferred text editor as an administrator. To do this, right-click on the text editor and select "Run as administrator." Then open the hosts file, which is usually located at `C:\Windows\System32\drivers\etc\hosts`. Add the following entry to the hosts file:

     ```
     VM_IP_ADDRESS your_name.com
     ```

     Replace `VM_IP_ADDRESS` with the actual IP address of your VM.

   - On Linux or macOS:
     Open a terminal and edit the hosts file using a text editor with superuser privileges, such as `sudo nano` or `sudo vim`. For example:

     ```
     sudo nano /etc/hosts
     ```

     Add the following entry to the hosts file:

     ```
     VM_IP_ADDRESS your_name.com
     ```

     Replace `VM_IP_ADDRESS` with the actual IP address of your VM.

2. **Save the Hosts File**:

   Save the hosts file after adding the entry. In most text editors, you can press `Ctrl` + `S` (or `Cmd` + `S` on macOS) to save the changes.

3. **Access "your_name.com"**:

   After saving the hosts file, you should be able to access "your_name.com" from your host machine's web browser, and it will display the `index.html` page from your VM.

   Open your web browser and enter the following URL in the address bar:

   ```
   http://your_name.com
   ```

   Your web browser should resolve "your_name.com" to the IP address of your VM and display the custom `index.html` page you created with your name.

By editing the hosts file on your host machine, you can map a custom hostname to your VM's IP address, allowing you to access the custom web page using the desired domain name.



## python-app-deployment
This repo contains Python applications to practice DevOps practice with these

Assignment Instruction
Fork the repo
Run Both Applications in localhost
Provide all the changes needed in configuration files to properly deploy it in localhost in the documentation
Deploy both applications in a VM, where the host will be the VM's IP
Access the application from the web browser
Provide all changes needed in configuration files to properly deploy it in a remote VM
Automate the whole process with shell script so that the project can be seamlessly deployed in local and remote server environment
Submit the link of the forked git repo which will contain all config and scripts along with the project code and documentation
Documentation could be a readme.md file or any pdf file
Note:
Project with db connection needs a db server with proper configuration to work properly. Prepare a db server and upload the dump file, which contains the data schema for the respective project.

Project Structure
Each Python application should be run inside a virtual environment
All dependencies should be listed in a file, commonly named requirements.txt
Before executing the program, the virtual environment should be created and activated
Before executing the program, all dependencies should be resolved by installing all packages listed in requirements.txt
Basic commands

- for deployment in the localhost first app
```
python --version
git clone https://github.com/obijzbo/python-app-deployment.git
cd python-app-deployment
python -m venv venv
venv\Scripts\activate
python.exe -m pip install --upgrade pip
cd python-fast-app
pip install -r requirements.txt
pip install flask
set FLASK_APP=main.py
set FLASK_ENV=development
pip install fastapi
pip install mysql-connector-python
pip install uvicorn
pip install python-multipart
uvicorn main:app --host 0.0.0.0 --port 8000

py main.py
```
- for active connections
```
netstat
```
# Docker Assignment - 1
-Write a Dockerfile for any project
- Make it multistage compatible
- Make it multiplatform compatible with buildx
- Push the image to the docker hub
- Write commands to
- Run containers from image
- Open a shell inside the container
- Submit the git repository with the project, Dockerfile, bash script if any, and documentation

# Docker commands for installation
### Update package lists
```
sudo apt-get update
```
### Remove existing Docker packages
```
sudo apt-get remove docker docker-engine docker.io containerd runc -y
```
### Install required packages for Docker installation
```
sudo apt-get install apt-transport-https ca-certificates curl software-properties-common -y
```
### Add Docker's official GPG key
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
### Add Docker repository
```
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
```
### Update package information with the new Docker repository
```
sudo apt-get update
```
### Install Docker CE (Community Edition)
```
sudo apt-get install docker-ce -y
```
### Check the status of Docker service
```
sudo systemctl status docker
```
