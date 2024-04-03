1. The first thing you want to do is update your arch linux. sudo pacman -Syu
2. Install vim by typing in the command sudo pacman -S vim
3. Install nginx by typing in command sudo pacman -S nginx. (if getting errors, do sudo nginx -t)
4. Create a new directory "/web/html/nginx-2420" that will act as your project root. The directory where your website documents will be stored. mkdir -p /web/html/nginx-2420
5.Backup your current nginx.conf file