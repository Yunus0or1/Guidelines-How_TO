# Django Production Server Host
 - Install Python using this command :
   ```
   sudo apt-get update
   sudo apt-get upgrade
   sudo apt-get install python3 pip3
   ```
   
 - Install MySQL server First Ubuntu
   Tutorial [link](https://support.rackspace.com/how-to/install-mysql-server-on-the-ubuntu-operating-system/)
   Commands are here.
   ```
   sudo apt-get install mysql-server
   sudo apt-get install libmysqlclient-dev
   sudo systemctl stop mysql
   sudo systemctl disable mysql
   ```
   
 - Install Virtual Environment 
   ```
   sudo apt-get install python3-virtualenv
   ```
   	
 - Install Django with other requirements 

   - Create a virtualenv inside the Django Project folder or where you want : 
     ```
     virtualenv -p python3 django_env
     ```
    - Activate it
      ```
      source django_env/bin/activate
      ```
    - Open up **settings.py** in Django project and if you use MySQL then use these lines in DB setting : 
      ```Python
      DATABASES = {
		'default': {
			'ENGINE': 'django.db.backends.mysql',
			'NAME': 'ecom',
			'HOST': '/opt/lampp/var/mysql/mysql.sock', #This is the mysql socket file from Xampp. Most Important
			'PORT': '', 
			'USER': 'root',
			'PASSWORD': '',
			#use 'HOST': '118.179.70.235','PORT': '3306','USER': 'ybazar','PASSWORD': 'cd30i4FyvZ8Ug2je', for Online Database and Ip would your IP. 3306 is port forwarded.
		}}
      ```		
    - Add these two lines in **settings.py**.
      ```Python
      # According to your location set Static files path. Keep notice if these files are not locked. Otherwise nginx will not serve them.
      STATIC_ROOT = '/home/yunus/Desktop/staticRootFile/'  	
		
      MEDIA_ROOT =os.path.join(BASE_DIR, "ecom","media")		# According to your location
      ```
    - Change these settings.
      ```
      DEBUG = False
      ALLOWED_HOSTS = ['*']  # Allowed all hosts. Change it to your IP and Domain name
      ```
    > Regardless of which version of Python you are using, when the virtual environment is activated, you should use the pip command (not pip3).
    
    - When you are in Virtual Environment install Django and other libraries :	
      ```
      pip install django 
      pip install gunicorn
      ```
    - Run these commands :
      ```
      pip install pymysql
      pip install mysqlclient
      pip install mysql-connector-python-rf
      ```
    - Bind gunicorn with wsgi :
      ```
      gunicorn --bind 0.0.0.0:8000 <folder_name_where_wsgi_file_exists>.wsgi # Example ecom.wsgi or myProject.wsgi
      ```	
    - If any problem persists to install mysqlclient install on virtual env such as in **AWS**
      ```
      sudo apt-get install python3.6-dev libmysqlclient-dev
      pip install mysqlclient
      ```

- To use Ubuntu MySQL. 
  - To load a database using command line:
    ```
    sudo mysql -u <username 'root'> -p <databasename> < <filename.sql '/home/yunus/Desktop/my.sql'>
    ```
  - To access grant to 'root@localhost' use this command
    ```
    sudo mysql
    ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'root'; // This would set user root with password root
    ```
 - Install and Run [Xampp](https://www.apachefriends.org/index.html) for Linux
   - Rename it xampp.run and type this commands :
     ```
     chmod 755 xampp.run
     sudo ./xampp.run -- install
     sudo /opt/lampp/lampp start
     sudo /opt/lampp/xampp stop	
     udo /opt/lampp/uninstall  
     ```





	


### Create a Gunicorn systemd Service File


	sudo nano /etc/systemd/system/gunicorn.service
	
	
	Copy paste these lines and set locations according to your config :
	
		[Unit]
		Description=gunicorn daemon
		After=network.target

		[Service]
		User=yunus
		Group=www-data
		WorkingDirectory=/home/yunus/Desktop/ecom
		ExecStart=/home/yunus/Desktop/ecom/django_env/bin/gunicorn --access-logfile - --workers 3 --bind unix:/home/yunus/Desktop/ecom/ecom.sock ecom.wsgi:application

		[Install]
		WantedBy=multi-user.target


		#ecom.sock will be created automatically
		
		
	Now write these :
	
		sudo systemctl start gunicorn
		sudo systemctl enable gunicorn
		
	Next, check for the existence of the ecom.sock file within your project directory // Or whatever you_name_it.sock exists
	
	

### Configure Nginx

	Install it 

		sudo fuser -k 80/tcp
		sudo fuser -k 443/tcp
		
		sudo apt-get install nginx
		
		
	Create a coniguration file using this command with the project name :
	
		sudo nano /etc/nginx/sites-available/ecom
		
		
	Copy-paste these and change location according to your config :
	
		server {
				server_name habibindustry.com www.habibindustry.com;

				location = /favicon.ico { access_log off; log_not_found off; }
				location /static/ {
					alias /home/yunus/Desktop/staticRootFile/;
				}

				location / {
					include proxy_params;
					proxy_pass http://unix:/home/yunus/Desktop/ecom/ecom.sock;
				}

				location /media/ {
					alias   /home/yunus/Desktop/ecom/ecom/media/;
				}
	
			}


	Test your Nginx configuration for syntax errors by typing:
	
		sudo nginx -t
		
	Run this command :
		
		sudo ln -s /etc/nginx/sites-available/ecom /etc/nginx/sites-enabled
		
	Go to /etc/nginx/ and delete 'Defualt' from both sites-enabled and sites-available
		
	Now write these commands :
	
		sudo systemctl restart nginx
		sudo ufw delete allow 8000
		sudo ufw allow 'Nginx Full'
		
### Let Python and Nginx access the staticfile and Mediafile properly. Write these commands :

	sudo 777 -R staticfile	
	sudo 777 -R mediafile	

### Installing SSL in Server Nginx
	
	sudo add-apt-repository ppa:certbot/certbot
	sudo apt-get install python-certbot-nginx
	sudo ufw enable
	sudo ufw allow 'Nginx Full'
	sudo ufw delete allow 'Nginx HTTP'
	sudo certbot --nginx -d habibindustry.com -d www.habibindustry.com
	


Four Important Links 

	SSL : https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-18-04
	
	Nginx + Django : https://www.digitalocean.com/community/tutorials/how-to-set-up-django-with-postgres-nginx-and-gunicorn-on-ubuntu-16-04
	
	Nginx + Django : https://jee-appy.blogspot.com/2017/01/deply-django-with-nginx.html
	
	Start Xampp on startup
	
	https://salitha94.blogspot.com/2017/08/how-to-start-xampp-automatically-in.html
	
	
Uninstall and Install pip3
	
	sudo python3 -m pip uninstall pip && sudo apt install python3-pip --reinstall
		




#### Debugging Rules :


1. First stop nginx, gunicorn.
2. Start server using python3 manage.py runserver.
3. Fix what has gone wrong.
4. Start gunicorn and type : sudo systemctl status gunicorn.
5. If everything is ok, type : sudo systemctl start gunicorn and sudo systtemctl start nginx.
6. HTTP Port 80 must be forwarded in TCP. Or use Default HTTP port forward. 
7. Check if MySQL xampp database is up or not. Stop Xampp apache server.
8. Check if ufw has all port forwarding like Port 80 and 443.





























