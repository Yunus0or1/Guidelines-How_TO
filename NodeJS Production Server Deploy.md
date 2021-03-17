
# Installation

 - Type these commands.
 
   ```
   sudo apt update
   sudo apt install npm
   cd <where index.js or server.js located>
   npm install
   sudo npm install pm2 -g
   pm2 start index.js --name=<any_name> --watch --ignore-watch="node_modules"
   pm2 startup  (copy paste the generated line such as sudo env PATH=$PATH:/usr/bin /usr/local/lib/node_modules/pm2/bin/pm2 startup systemd -u ubuntu --hp /home/ubuntu --service-name=<your_name>)
   pm2 save
   sudo reboot
   ```
 - To check list.
   ```
   pm2 list
   ```
 - To Delete app.
   ```
   pm2 delete <APP_NAME>
   ```

# Add Nginx with pm2

 > pm2 loads the payment server locally in any port such as 8586. Nginx is connected with the pm2 server in any port such as 8587. So we access 8587 port from outside.
  
  - First type this command.
    ```
    sudo nano /etc/nginx/sites-available/<any_file_name>
    ```
  - Copy paste these.
    ```
    upstream my_local_server {
       server 127.0.0.1:8586;
       keepalive 64;
    }

      server {
          listen 8587;
          server_name <server_ip>;
          root </home/location where index.js or server.js is locatated/>;

          location / {
              proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
              proxy_set_header X-Real-IP $remote_addr;
              proxy_set_header Host $http_host;

              proxy_http_version 1.1;
              proxy_set_header Upgrade $http_upgrade;
              proxy_set_header Connection "upgrade";

              proxy_pass http://my_local_server/;
              proxy_redirect off;
              proxy_read_timeout 240s;
      }

    }
    ```
  
  
  
  
  
  
  
  
  
  
  
  
  
  
