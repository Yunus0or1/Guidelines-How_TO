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
   BROKER_URL = 'redis://localhost:6379'
   CELERY_RESULT_BACKEND = 'redis://127.0.0.1:6379/'
   CELERY_ACCEPT_CONTENT = ['application/json']
   CELERY_TASK_SERIALIZER = 'json'
   CELERY_RESULT_SERIALIZER = 'json'
   CELERY_TIMEZONE = 'UTC'
   ```   






































