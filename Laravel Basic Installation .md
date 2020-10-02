# Laravel Basic Installation

 - Install Xaamp. Google for it.
 - Install Composer. Google **Composer Laravel** or hit this [link](https://laravel.com/docs/4.2)
 - To start a project open CMD and run this command.
   ```
   composer create-project laravel/laravel your-project-name 4.2.* 
   ```

# Reinstall laravel project from Github

When upload laravel project to Github, git ignores all the dependencies and .env file. So these must be installed manually. After cloning
the project open CMD and cd to that directory. Then type these commands.

```
composer install
composer dump-autoload
copy .env.example .env  [To copy .env file]
php artisan key:generate
php artisan migrate
php artisan serve
```
Go to localhost:8000
    
> To be noticed It can not be guranteed that these commands will run without any error.There is problem with different versions of Laravel.





