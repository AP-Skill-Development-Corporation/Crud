## CRUD OPEARATIONS
CRUD stands for Create, Read, Update & Delete. These are the four basic operations which are executed on Database Models. We are developing a web app which is capable of performing these operations.


![](https://github.com/lavanya-Mercy/Crud/blob/master/Crud_imgs/curddd.jpg) 

**Create**   – create or add new entries in a table in the database. <br>
**Retrieve** – read, retrieve, search, or view existing entries as a list(List View) or retrieve a particular entry in detail.<br>
**Update**   – update or edit existing entries in a table in the database. <br>
**Delete**   – delete, deactivate, or remove existing entries in a table in the database. <br>


Majority of applications on the internet are CRUD applications. For example – Facebook uses CRUD operations to save your data on their database. You can change your profile picture that means perform the update operation. Of course, you can see the data in-app or browser which is read operation. Also, you can delete your Facebook account which is delete operation.

Let’s say we want to make our site a platform where a user can open an Account. Nothing complex, we’ll just let a user add, edit and delete the Books. Let’s get started.

### Making CRUD application
##### 1. Create a new project by executing the following command <br>
 	 ```django-admin startproject ProjectName```
##### 2. Creating new App 
Move to the directory of manage.py file and make a new app <br>
  ```python manage.py startapp AppName``` 
  
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
      'AppName',  
     ] 
```

  
#####  3. Making Model Forms in app
A Form class describes a form and determines how it works and appears.In a similar way that a model class’s fields map to database fields, a form class’s fields map to HTML form <input> elements.

For the above Registraion model, which we could use to implement “Registraion” functionality on our website: First we need to create froms.py file in our app location and import Register model class from models.py

**`forms.py`**
    
```python
   from django.forms import ModelForm
   from crud.models import Register
   class registrationform(ModelForm):
       class Meta:
           model = Register
           fields = '__all__'
```
We need to import Django forms first (from django import forms) and our Register model (from .models import Register). Next, we have class Meta, where we tell Django which model should be used to create this form (model = Register). Finally, we can say which field(s) should end up in our form. In this scenario if we want only few fields then metion them in a list formate.


##### 5. Registering Model in django Admin
Here we are editing admin.py existing in app folder. Import the model you want to register in the admin.<br>
**`admin.py`**
```python
from django.contrib import admin
from crud.models import Register

admin.site.register(Register)
```
##### 6. Sync with Database
* To implement all of this, run these commands in the command line

* Makemigrations : It is used to create a migration file that contains code for the tabled schema of a model. <br>
	```python manage.py makemigrations```

* Migrate : It creates table according to the schema defined in the migration file. <br>
	```python manage.py migrate```

##### 7. Making Views Function for Django crudApp
* The view functions are our actual CRUD operations in Django. Now, we are editing views.py in app folder

###### Read Data : 

**`views.py`**
```python
def details(request):
	data = Register.objects.all()
	return render(request,'crud/details.html',{'data':data})
```


###### Update Data : 

**`viwes.py`**
```python
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

**`viwes.py`**
```python
def delete(request,id):
	ob = Register.objects.get(id=id)
	if request.method == 'POST':
		ob.delete()
		return redirect('/crud/details')
	return render(request,'crud/msg.html',{'info':ob})
```


##### 8. Enabling Templates

> **_NOTE:_** Here we are using Bootstrap 4

**`details.html`**
```
{% load static %}
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
  	<meta name="viewport" content="width=device-width, initial-scale=1">
	<title>Details Page</title>
	<link rel="stylesheet" type="text/css" href="{% static 'css/bootstrap.min.css' %}">
	<script type="text/javascript" src="{% static 'js/bootstarp.min.js' %}"></script>
</head>
<body>
	<div class="container">
		<div class="row justify-content-left">
			<div class="col-sm-8">
				<div class="card">
					<div class="card-header">
					User Details
					</div>
				<div class="card-body">
			<table class="table table-striped responsive ">
				{% for row in data %}
					<tr>
					<td>{{row.id}}</td>
					<td>{{row.firstName}}</td>
					<td>{{row.lastName}}</td>
					<td>{{row.emailId}}</td>
					<td><a class='btn btn-info'href="{%url 'edit' row.id %}">Update</a></td>
					<td><a class='btn btn-info'href="{%url 'delete' row.id %}">Delete</a></td>
					</tr>
				{% endfor %}
			</table>
		     </div>
		</div>
	    </div>
      </div>
</div>
</body>
</html>
```



**`edit/id.html`**
```
<!DOCTYPE html>
<html>
<head>
	<title>Edit Page</title>
</head>
<body>
	<form action="{% url 'edit' data.id %}" method="POST">
	{% csrf_token %}
	{{ form.as_p }}
	<button type="submit">update</button>
	</form>
</body>
</html>
```

**`message.html`**
```
{% load static %}
<!DOCTYPE html>
<html>
<head>
	<title>User Form</title>
	<link rel="stylesheet" type="text/css" href="{% static 'css/bootstrap.min.css' %}">
	<script type="text/javascript" src="{% static 'js/bootstarp.min.js' %}"></script>
</head>
<body>
	<div class="container">
		<div class="row justify-content-left">
			<div class="card">
				<div  class="card-body">
					<form action="{% url 'delete' info.id %}" method="POST">
		{% csrf_token %}
	<h2>Are you sure to delete {{ info.firstName }}</h2>
	<input class='btn btn-warning' type="submit" name="submit" value="Delete">
	<a href="{% url 'details' %}" class="btn btn-info">Cancel</a>	
</form>
				</div>
			</div>
		</div>
	</div>
</body>
</html>

```


> **_NOTE:_** Add the {% csrf_token %} to every Django template you create that uses POST to submit data. This will reduce the chance of forms being hijacked by malicious users.


###### Designing URLs 
To present data we need to write a ‘views’ which is mapped to a URL pattern. Editing urls.py allows URL patterns to be defined.

In the main url file we have to include our apps url file .For that we have to add the url.py file path
**`urls.py`**
```python
from django.contrib import admin
from django.urls import path,include
urlpatterns = [
    path('admin/', admin.site.urls),
    path('crud/',include('crud.urls')),

]
```
Now in our app we have to create a urls.py file,and in that file we have to add the html files path.

**`urls.py`**
```python
from django.contrib import admin
from django.urls import path
from crud import views
urlpatterns = [
	path('details/',views.details,name='details'),
	path('edit/<int:id>',views.edit,name='edit'),
	path('delete/<int:id>',views.delete,name='delete'),

]
```

###### Browsing the web pages 
Open web page with localhost and required URL given in your project  urls.py file.

``` http://127.0.0.1:8000/crud/details/ ```

![](https://github.com/lavanya-Mercy/Crud/blob/master/Crud_imgs/details.PNG)

``` http://127.0.0.1:8000/crud/edit/2 ```

![](https://github.com/lavanya-Mercy/Crud/blob/master/Crud_imgs/update.PNG)

``` http://127.0.0.1:8000/crud/delete/2 ```


![](https://github.com/lavanya-Mercy/Crud/blob/master/Crud_imgs/del.PNG)



