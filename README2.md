1. First thing you want to do is to update your system. sudo pacman -Syu. This command updates your Arch Linux system to the most up-to-date.

```sudo pacman -Syu```

3. After updating your Arch Linux system, you want to install the firewall. This command sudo pacman -Su ufw will install a Uncomplicated firewall. Here is a screenshot to show what it looks like after it finishes updating.

``` Sudo pacman -Su ufw```
![[Screenshot 2024-04-10 125059.png]]

   UFW is a program that makes it a little easier to manage a [netfilter](https://netfilter.org/) firewall. UFW actually manages nftables or iptables, which make use of netfilter which is part of the Linux kernel

3. To check if UFW was installed successfully, use the command sudo ufw status verbose. It should show status inactive.

```sudo ufw status verbose```

5. If there is a reason that it does not show status inactive, and shows some error message, you have to reboot your system. To do that, type in sudo systemctl reboot to reboot Arch Linux in the backend. It should take 2 minutes to reboot. After it has been rebooted, go back to step 4 and check again if UFW status is inactive.

```sudo systemctl reboot```. 

6. After rebooting your system and checking UFW status, you can check a list of applications connected. Use ```sudo ufw app list``` to see a list of applications.
![[Screenshot 2024-04-10 133512.png]]
```sudo ufw app list```

8. Now you have to allow some connections. Using sudo ufw allow allows connections to connect to our servers. Now allow the connections sudo ufw allow ssh, sudo ufw allow 22, sudo ufw allow 80, sudo ufw allow HTTP, sudo ufw allow SSH. This allows certain connections and HTTP connect to connect to our servers.

```
sudo ufw allow ssh 
sudo ufw allow 22 
sudo ufw allow 80 
sudo ufw allow HTTP 
sudo ufw allow SSH
```

7. Now allowing the connections, we can enable our UFW firewall. The command sudo ufw enable will turn on UFW. It should say firewall is active and enabled on system start up.

```sudo ufw enable```
![[Pasted image 20240410140146.png]]

9.  Now enable ufw on start up. sudo systemctl enable ufw.

```sudo systemctl enable ufw```

8. Now, go ahead and reboot your system again. Sudo systemctl reboot

```Sudo systemctl reboot```

9. After system has been rebooted, check UFW status. sudo ufw status verbose. It should list out some connections that are allowed.

![[Screenshot 2024-04-10 134816.png]]

```sudo ufw status verbose```

10. if you allow a service that you didn't mean to, you can remove it with

```
sudo ufw delete allow
```

11. Now that UFW firewall has been set up, we can now set up our proxy servers. Using our previous nginx server, we are going to add some settings to the configuration. Use the command sudo vim /etc/nginx/sites-available/nginx-2420 to access the config file. 

```
sudo vim /etc/nginx/sites-available/nginx-2420
```
12. There is not much to change except to add 
```
 location /api {
        # Define the reverse proxy settings
        proxy_pass http://127.0.0.1:8080;
        proxy_http_version 1.1;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
```
Do not forget to change the proxy pass to your ip address

13. Now you can test if your server works with proxies, either use postman or the curl command in the windows powershell. For curl, do the command ```curl http://146.190.12.184``` change the ip address to your server. Now add `curl http://146.190.12.184/hey` to test it.