## Crud
CRUD stands for Create, Read, Update & Delete. These are the four basic operations which are executed on Database Models. We are developing a web app which is capable of performing these operations.


![](https://github.com/lavanya-Mercy/Crud/blob/master/curddd.jpg) 

**Create**   – create or add new entries in a table in the database. <br>
**Retrieve** – read, retrieve, search, or view existing entries as a list(List View) or retrieve a particular entry in detail.<br>
**Update**   – update or edit existing entries in a table in the database. <br>
**Delete**   – delete, deactivate, or remove existing entries in a table in the database. <br>

Operation|Sql|Http
----|----|----
Create|INSERT| PUT/POST
Read|SELECT|GET
Update|UPDATE|PUT/PATCH
Delete|DELETE|DELETE




Let’s say we want to make our site a platform where a user can open an Account. Nothing complex, we’ll just let a user add, edit and delete the Books. Let’s get started.

### Making CRUD application
##### Create a new project by executing the following command <br>
  ```django-admin startproject crudProject```
##### Creating new App 
* Move to the directory of manage.py file and make a new app <br>
  ```python manage.py startapp crudApp```
	* Don’t forget to add your new app to the Installed app. Append crudApp/settings.py as follows <br>

		```
		  INSTALLED_APPS = [  
		      'django.contrib.admin',  
		      'django.contrib.auth',  
		      'django.contrib.contenttypes',  
		      'django.contrib.sessions',  
		      'django.contrib.messages',  
		      'django.contrib.staticfiles',  
		      'crudApp',  
		     ] 
		```
  
##### Making Models for crudApp
  * We are making a model or database table for our app.
  **`models.py`**
```python
from django.db import models

class Register(models.Model):
    firstName = models.CharField(max_length=100)
    lastName = models.CharField(max_length=100)
    emailId = models.MailField(null = True)
    phoneNo = models.CharField(max_length=10)
    age = models.IntegerField(null=True)
```
  
	

  
#####  Making Model Forms in app

* We also need to create a simple form to perform CRUD operations. Create a new python file inside your app and name it 		   forms.py. Append the following code to it.<br>
    
	```
		   from django.forms import ModelForm
		   from appName.models import userdata
		   class userform(ModelForm):
		   class Meta:
			model = userdata
			fields = '__all__'
	```

##### Registering Model in django Admin
* Here we are editing admin.py existing in app folder. Import the model you want to register in the admin.
	```
	   from crudApp.models import userdata
	   admin.site.register(userdata)
	```
##### Makemigrations and migrate
* To implement all of this, run these commands in the command line

* **makemigrations** : It is used to create a migration file that contains code for the tabled schema of a model. <br>
	```python manage.py makemigrations```

* **migrate** : It creates table according to the schema defined in the migration file. <br>
	```python manage.py migrate```





