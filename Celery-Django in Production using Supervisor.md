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
   
 - Visit **__init__.py** file in the same directory and paste these
   ```
   from __future__ import absolute_import

   # This will make sure the app is always imported when
   # Django starts so that shared_task will use this app.
   from .celery import app as celery_app

   __all__ = ('celery_app',)
   ```   
 - Visit **settings..py** file in the same directory and paste these
   ```
   CELERY_BROKER_URL = 'redis://localhost:6379'
   CELERY_RESULT_BACKEND = 'redis://127.0.0.1:6379/'
   CELERY_ACCEPT_CONTENT = ['application/json']
   CELERY_TASK_SERIALIZER = 'json'
   CELERY_RESULT_SERIALIZER = 'json'
   CELERY_TIMEZONE = 'UTC'
   ```   
 - Use this command to check if celery is working
   ```
   celery -A your_project_name worker -l info
   ```
 - Use this command to check if celery beat also known as periodic scheduler is working
   ```
   celery -A your_project_name beat -l info
   ```
 - Now create an Django app, register it in **settings.py** and now inside the app folder create a file named **tasks.py**. In this file you have to add all your celery tasks
   ```
   from __future__ import absolute_import, unicode_literals
   from celery import shared_task
   
   
   @shared_task(name = "print_msg_main")
   def print_message(message, *args, **kwargs):
    print(f"Celery is working!! Message is {message}")
   ```
 - In the **celery.py** file, add these lines to do task periodically
   ```
   app.conf.beat_schedule = {
       'print-message-ten-seconds': {
           # Task Name (Name Specified in Decorator)
           'task': 'print_msg_main',  
           # Schedule      
           'schedule': 10.0,
           # Function Arguments 
           'args': ("Hello",) 
       },
   } 
   ```
 - Now write these two commands to start beat and worker. These two must be started simultaneously. Beat would push task to worker and Worker would execute it.
   ```
   celery -A proj_name beat -l info --logfile=celery.beat.log
   celery -A proj_name worker -l info --logfile=celery.log
   ```
   
  - Sometime worker in windows may throw ValueError due to OS. So run this worker command instead of the first one for the worker.
   ```
   celery -A proj_name worker --pool=solo -l info --logfile=celery.log
   ```
   
   This would start the tasks in period motion

 - To install Celery in production run this first.
   ```
   sudo apt-get install supervisor
   sudo supervisord
   ```
   Usually supervisor gets auto started. So using ***sudo supervisord*** command may throw error on same port opening.
   
 - Run this command to open conf file for celery worker
   ```
   sudo nano /etc/supervisor/conf.d/app-name-worker.conf
   ```
 - Edit and Copy these lines
   ```
   [program:your-app-name-worker]
   command=/path_to_virtual_env/bin/celery -A project_name worker -l info
   directory=/path_to_your_project_name/
   user= <root_user_name>
   group=www-data
   autostart=true
   autorestart=true
   stdout_logfile=/path_to_store_log/celery-worker.log
   redirect_stderr=true
   wantedBy=multi-user.target
   ```
 - Run this command to open conf file for celery beat
   ```
   sudo nano /etc/supervisor/conf.d/app-name-beat.conf
   ```
 - Edit and Copy these lines
   ```
   [program:your-app-name-beat]
   command=/path_to_virtual_env/celery -A project_name beat -l info
   directory=/path_to_your_project_name/
   user= <root_user_name>
   group=www-data
   autostart=true
   autorestart=true
   stdout_logfile=/path_to_store_log/celery-beat.log
   redirect_stderr=true
   wantedBy=multi-user.target
   ```
- Supervisor commands to check
  ```
  sudo service supervisor restart
  sudo supervisorctl restart <name>
  sudo service supervisor stop
  sudo service supervisor start
  sudo supervisorctl reread
  sudo supervisorctl update
  sudo supervisorctl start app2
  sudo supervisorctl status app2
  ```

[Tutorial Link](https://nickmccullum.com/celery-django-periodic-tasks/) | [Supervisor Commands](https://www.onurguzel.com/supervisord-restarting-and-reloading/) | [ReadMe On Supervisor](https://gist.github.com/mau21mau/9371a95b7c14ddf7000c1827b7693801)




























