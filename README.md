# Django Course >> My Site <<

## Setting up the starting project
```bash
django-admin startproject my_site 
```

Adding a new App 

```bash
python manage.py startapp blog
```

We can enable the development server using:
 ```bash
python manage.py runserver
 ```

## 1.- Create the urls.py file inside the app folder

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.starting_page, name="starting-page"),
    path('posts', views.posts, name="post-page"),
    path('posts/<slug:slug>', views.post_detail, name="post-detail-page")
]
```

## 2.- In the viwes.py file create the functions 

```python
from django.shortcuts import render

# Create your views here.

def starting_page(request):
    pass

def posts(request):
    pass

def post_detail(request):
    pass
```

## 3.- In the main urls.py file add:

```python
from django.contrib import admin
from django.urls import path, include # <-- new

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include("blog.urls")) # <-- new
]
```