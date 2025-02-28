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
## 8.- Create your HTML FILE index.html

```django
{% extends "base.html" %}

{% block title %}
My blog
{% endblock title %}

{% block content %}
<header>
<h1><a href="">Samuel's Blog</a></h1>
<nav>
    <a href="">All Post</a>
</nav>
</header>

<section id="welcome">
    <header>
        <img src="" alt="Sam - the aoutor of this blog">
        <h2>SAMUEL'S BLOG</h2>
    </header>
    <p>Hi, I am Sam and I love coding</p>
</section>
{% endblock content %}
```

## 9.- Creation of the static files 

Create this path for your base css file

```bash
my_site/templates/app.css
```

And other one for you app:
```bash
my_site/blog/static/blog/index.css
```

## 10.- To make django aware of these static files and app set in my_site/my_site/settings.py

```python

STATIC_URL = 'static/'

STATICFILES_DIRS = [    # <-- new
    BASE_DIR / "static" # <-- new
]                       # <-- new
```

## 11.- For load your css files in the html add: 

```django
{% extends "base.html" %} 
{% load static %}   # <-- new

{% block title %}
My blog
{% endblock title %}

{% block css_files %}   # <-- new
    <link rel="stylesheet" href="{% static "blog/index.css" %}">    # <-- new
{% endblock css_files %}    # <-- new

{% block content %}
<header>
<h1><a href="">Samuel's Blog</a></h1>
<nav>
    <a href="">All Post</a>
</nav>
</header>

<section id="welcome">
    <header>
        <img src="" alt="Sam - the aoutor of this blog">
        <h2>SAMUEL'S BLOG</h2>
    </header>
    <p>Hi, I am Sam and I love coding</p>
</section>
{% endblock content %}
```

## 12.- Create a Folder for the images in:
```bash
my_site/blog/static/blog/images/
```
## 13c.- Add the images like in this example: 
```django
<img src="{% static "blog/images/montain.png" %}" alt="Mountain Hiking" />
```