## CRUD OPEARATIONS
CRUD stands for Create, Read, Update & Delete. These are the four basic operations which are executed on Database Models. We are developing a web app which is capable of performing these operations.


![](https://github.com/lavanya-Mercy/Crud/blob/master/curddd.jpg) 

**Create**   – create or add new entries in a table in the database. <br>
**Retrieve** – read, retrieve, search, or view existing entries as a list(List View) or retrieve a particular entry in detail.<br>
**Update**   – update or edit existing entries in a table in the database. <br>
**Delete**   – delete, deactivate, or remove existing entries in a table in the database. <br>


Majority of applications on the internet are CRUD applications. For example – Facebook uses CRUD operations to save your data on their database. You can change your profile picture that means perform the update operation. Of course, you can see the data in-app or browser which is read operation. Also, you can delete your Facebook account which is delete operation.

Let’s say we want to make our site a platform where a user can open an Account. Nothing complex, we’ll just let a user add, edit and delete the Books. Let’s get started.

### Making CRUD application
##### 1. Create a new project by executing the following command <br>
 	 ```django-admin startproject crudProject```
##### 2. Creating new App 
Move to the directory of manage.py file and make a new app <br>
  ```python manage.py startapp crudApp``` 
  
Don’t forget to add your new app to the Installed app. Append crudApp/settings.py as follows <br>
**`settings.py`** 

```python
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

  
#####  3. Making Model Forms in app
We also need to create a simple form to perform CRUD operations. Create a new python file inside your app and name it 		   forms.py. Append the following code to it.<br>

**`forms.py`**
    
```python
   from django.forms import ModelForm
   from appName.models import userdata
   class userform(ModelForm):
   class Meta:
	model = userdata
	fields = '__all__'
```

##### 5. Registering Model in django Admin
Here we are editing admin.py existing in app folder. Import the model you want to register in the admin.<br>
**`admin.py`**
```python
from crudApp.models import userdata
admin.site.register(userdata)
```
##### 6. Sync with Database
* To implement all of this, run these commands in the command line

* Makemigrations : It is used to create a migration file that contains code for the tabled schema of a model. <br>
	```python manage.py makemigrations```

* Migrate : It creates table according to the schema defined in the migration file. <br>
	```python manage.py migrate```

##### 7. Making Views Function for Django crudApp
* The view functions are our actual CRUD operations in Django. Now, we are editing views.py in app folder

###### Update Data : 

**`admin.py`**
	```
	def edit(request,id):
		data = Register.objects.get(id=id)
		if request.method =='POST':
			form = registrationform(request.POST,instance=data)
			if form.is_valid():
				form.save()
				return redirect('/crud/details')
		form = registrationform(instance=data)
		return render(request,'crud/edit.html',{'form':form,'data':data})
	```


###### Delete Data :




