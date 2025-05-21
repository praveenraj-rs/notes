```py
1. django-admin startproject mysite
2. python3 manage.py runserver
3. python3 manage.py startapp posts
```
### Views
```py
from django.http import HttpResponse

def home(request):
    return HttpResponse("Hello, world!")
```
