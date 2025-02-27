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

## 4.- Inside your app folder create another folder called templates and another   one for your html files

In this case it will be:
```bash
my_site/blog/templates/blog
```

## 5.- Create another dir called templates for your base html

In this case ot will be:
```bash
my_site/templates/
```

## 6.- Create your html base template

```django
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{% block title %}{% endblock  %}</title>
    {% block css_files %}{% endblock  %}
</head>
<body>
    {% block body %}{% endblock  %}
</body>
</html>
```

## 7.- To make django aware of these templates and app set in my_site/my_site/settings.py

```python

INSTALLED_APPS = [
    'blog',      #<--- new
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]

TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [
            BASE_DIR / "templates"    # <--- new
        ],
        'APP_DIRS': True, 
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
```
