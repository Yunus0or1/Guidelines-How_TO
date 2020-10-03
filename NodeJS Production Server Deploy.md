
# Installation

 Type these commands.
 
 ```
 cd <where index.js or server.js located>
 sudo apt install npm
 npm install
 sudo npm install pm2 -g
 pm2 start index.js --name=<any_name> --watch --ignore-watch="node_modules"
 pm2 startup 
 > copy paste the generated line such as
 sudo env PATH=$PATH:/usr/bin /usr/local/lib/node_modules/pm2/bin/pm2 startup systemd -u ubuntu --hp /home/ubuntu --service-name=<your_name>)
 pm2 save
 sudo reboot
 ```


npm install pm2 -g
pm2 start app.js --name= <Name> --watch
pm2 save

Add pm2 in Systemmd

pm2 startup
<COPY THE COMMAND WITH THIS INSTRUCTION> --service-name <name>

You may need to reboot:
sudo reboot

To check list
pm2 list

To Delete app
pm2 delete <APP_NAME>



ADD NGINX

sudo nano /etc/nginx/sites-available/<Name>

upstream <Name> {
    # Nodejs app upstream
    server 127.0.0.1:3000;
    keepalive 64;
}
 
# Server on port 80
server {
    listen 80;
    server_name hakase-node.co;
    root /home/yume/hakase-app;
 
    location / {
        # Proxy_pass configuration
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $http_host;
        proxy_set_header X-NginX-Proxy true;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_max_temp_file_size 0;
        proxy_pass http://hakase-app/;
        proxy_redirect off;
        proxy_read_timeout 240s;
    }
}
