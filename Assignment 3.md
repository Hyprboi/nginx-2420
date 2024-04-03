1. The first thing you want to do is update your arch linux. ```sudo pacman -Syu``` What it does is update arch linux. Sudo gives the user admin privilages. Pacman is package manager. and -Syu is 
2. Install vim by typing in the command ```sudo pacman -S vim``` Vim is a text editor that allows us to type in syntax.
3. Install nginx by typing in command ```sudo pacman -S nginx```. (if getting errors, do ```sudo nginx -t```)
4. Create a new directory "/web/html/nginx-2420" that will act as your project root. The directory where your website documents will be stored. ```mkdir -p /web/html/nginx-2420``` mkdir create folders.
5. Go to /etc/nginx/sites-available ```cd /etc/nginx/sites-available```
6. type in ls to see if there is a sites-available folder. If not, create it. ```sudo mkdir sites-available```. Also create a site-enabled folder. ```sudo mkdir sites-enabled```
6. create a new configuration file in the sites-available folder. ```sudo vim nginx-2420```
7. Create a new server block inside the file. input into the file in vim, enter insert mode.
```
    server { 
    listen 80; # Listen for incoming connections on port 80
    server_name 24.144.81.66; # Specify the server name or IP address that this server block will respond to

    root /web/html/nginx-2420; # Define the root directory where the website documents are stored
    index index.html index.html; # Define the default index files to serve if no specific file is requested

    location / { # Configuration for handling requests to the root directory '/'
        try_files $uri $uri/ =404; # Try to serve the requested file, and if it doesn't exist, return a 404 error
    }
}
```

8. exit insert mode by pressing the esc key. type :wq to save and quit file.
9. Now go the /web/html/nginx-2420 folder. type cd to enter root folder. then ```cd /web/html/nginx-2420```
10. create a html file named index.html. ```sudo vim index.html```
11. Enter insert mode and add in 
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2420</title>
    <style>
        * {
            color: #db4b4b;
            background: #16161e;
        }
        body {
            display: flex;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
        }
        h1 {
            text-align: center;
            font-family: sans-serif;
        }
    </style>
</head>
<body>
    <h1>All your base are belong to us</h1>
</body>
</html>
```
Exit insert mode and type in :wq This is your html file and should display All your base are belong to us.
12. Now add a symbolic link to your /etc/nginx/sites-available/nginx-2420 and /etc/nginx/sites-enabled/
```sudo ln -s /etc/nginx/sites-available/nginx-2420 /etc/nginx/sites-enabled/```
13. Check for errors in code. ```sudo nginx -t```
14. Now you can enable nginx. Type in ```sudo systemctl start nginx``` systemctl
15. Enable nginx on start up. ```sudo systemctl enable nginx``` enable allows nginx to run on start up.
16. Check if status is on by ```sudo systemctl status nginx``` status checks the status of the service.
17. If there are any errors on start up, you can also use ```journalctl -xeu nginx.service```
18. Log into your website by entering the ip address. for instance, type in the url 24.144.81.66
19. Should be able to see the html page.



