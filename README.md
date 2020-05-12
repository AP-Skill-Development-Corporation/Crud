## Crud
CRUD stands for Create, Read, Update & Delete. These are the four basic operations which are executed on Database Models. We are developing a web app which is capable of performing these operations.


![](https://github.com/lavanya-Mercy/Crud/blob/master/curddd.jpg) 

**Create**   – create or add new entries in a table in the database. <br>
**Retrieve** – read, retrieve, search, or view existing entries as a list(List View) or retrieve a particular entry in detail.<br>
**Update**   – update or edit existing entries in a table in the database. <br>
**Delete**   – delete, deactivate, or remove existing entries in a table in the database. <br>

Let’s say we want to make our site a platform where a user can add their favorite Books. Nothing complex, we’ll just let a user add, edit and delete the Books. Let’s get started.

### Making CRUD application
* Create a new project by executing the following command <br>
  ```django-admin startproject crudProject```
* Move to the directory of manage.py file and make a new app <br>
  ```python manage.py startapp crudApp```
* Don’t forget to add your new app to the Installed app. Append crudApp/settings.py as follow,
  ```INSTALLED_APPS = [  
      'django.contrib.admin',  
      'django.contrib.auth',  
      'django.contrib.contenttypes',  
      'django.contrib.sessions',  
      'django.contrib.messages',  
      'django.contrib.staticfiles',  
      'crudApp',  
     ] ```
  



