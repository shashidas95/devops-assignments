# assignments-

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

9. To install the Nginx web server in a virtual machine (VM) and access the welcome page
 ```
 sudo apt update
 sudo apt install nginx
 sudo systemctl start nginx
 sudo systemctl status nginx
 ```
