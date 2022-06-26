
# Anugular/React Deployment


- Install Node And Angular:
  ```
  sudo apt install python-software-properties
  curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
  sudo apt install nodejs
  sudo npm install -g @angular/cli
  ```
- Go to project folder where you can find **package.json** file. Open a terminal inside that folder. Type
  ```
  sudo npm install
  npm run build --prod
  ```
  You will find a **dist** folder generated that is final build version for that Angular Project.
  
- Type this command in terminal:
  ```
  cd /etc/nginx/sites-available
  sudo nano admission-angular
  ```
- Copy Paste this lines in new conf file
  ```
  server {
          listen 80;
          server_name <domain name or IP>;

          location / {

          root <your_project_folder>/dist/admission-portal;
          #root /home/yunus/Desktop/addmission-angular/admission-portal/dist/admission-portal;

          index index.html index.htm;
          try_files $uri $uri/ /index.html;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection "upgrade";

          }
  }

  ```
 - Now type this command in terminal:
   ```
   sudo ln -s /etc/nginx/sites-available/admission-angular /etc/nginx/sites-enabled
   sudo nginx -t
   ```
   
   If no error then the config is good.
   
 ***Remember to port forward in ufw firewall if necessary.***
