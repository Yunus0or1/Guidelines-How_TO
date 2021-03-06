# Django Basic Installation Guide

 - Install python 3.6.39(32 bit) or 3.6.2(64 bit) with ticked on Add to the path.
 - Install pycharm or not , it is upto you.
 - To install Django run this command
   ```
   pip install Django
   ```
 - Run the command to create project.
   ```
   Django-admin startproject prac
   ```
 - To run the server go to the directory of the file and type this command.
   ```
   python manage.py runserver
   ```
 - To create app go to the directory of the file and type this command.
   ```
   python manage.py startapp hello
   ```
 - To render template first create a folder anywhere and then go to **settings.py **, find TEMPLATES and set the directory
 - To migrate database use these commands.
   ```
   python manage.py makemigrations
   python manage.py migrate
   ```
 - To istall Database xampp in Django :
   - Run these commands
     ```
     pip install MySQL-python
     pip install pymysql
     pip install mysqlclient
     pip install mysql-connector-python-rf
     pip install "mysqlclient==1.3.12"
     ```
     
     ```Python
     DATABASES = {
		'default':  
			 {
		'ENGINE': 'django.db.backends.mysql',
		'NAME': 'DB_NAME',
		'HOST': '127.0.0.1',
		'PORT': '3306',
		'USER': 'root',
		'PASSWORD': '',
			  }  
		 }
     ```
 - To add ImageField in Django Model run this command.
   ```
   pip install pillow
   ```
 - To install Crypto package try this.
   ```
   pip install pycryptodome  / pip install pycrypto
   ```


