# Celery-Django in Production using Supervisor Installation Guide
 - Install Redis. In Windows download the files and run it. In Linux:
   ```
   sudo apt install redis-server
   ```
 - To install Celery run this command
   ```
   pip install celery
   ```
 - To install redis-python run this command
   ```
   pip install redis
   ```
 - Create a file named **celery.py** in the main Django project directory where **settings.py** is located
   ```
   from __future__ import absolute_import, unicode_literals
   import os
   from celery import Celery

   # set the default Django settings module for the 'celery' program.
   os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'project_name.settings')
   # os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'ezeedrop_scheduler.settings')

   app = Celery('any_name')
   # app = Celery('ezeedrop_scheduler',broker='redis://127.0.0.1:6379/')

   # Using a string here means the worker doesn't have to serialize
   # the configuration object to child processes.
   # - namespace='CELERY' means all celery-related configuration keys
   #   should have a `CELERY_` prefix.

   app.config_from_object('django.conf:settings', namespace='CELERY')
   
   # Load task modules from all registered Django app configs.
   app.autodiscover_tasks()

   @app.task(bind=True)
   def debug_task(self):
   	print('Request: {0!r}'.format(self.request))
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


