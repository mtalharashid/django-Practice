🚀 1. Installation & Environment Setup
1. Create & Activate Virtual Environment
# Create virtual environment
python -m venv venv

# Activate (Windows)
venv\Scripts\activate

# Activate (Mac/Linux)
source venv/bin/activate

📦 2. Install Django
pip install django


Verify installation:

django-admin --version

🏗️ 3. Create First Django Project
django-admin startproject myproject


Move into the project:

cd myproject


Run the server to test:

python manage.py runserver

🧩 4. Create First App
python manage.py startapp myapp


Add the app to settings.py:

INSTALLED_APPS = [
    ...
    'myapp',
]

🌐 5. Create First URL
Project-level URL (myproject/urls.py):
from django.contrib import admin
from django.urls import path
from myapp import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', views.home, name='home'),
]

👁️ 6. Create First View (myapp/views.py)
from django.http import HttpResponse

def home(request):
    return HttpResponse("Hello, Django!")

📄 7. Create First HTML Template (Optional)

Create folder:

myapp/
 └── templates/
       └── home.html


home.html:

<h1>Hello Django Template</h1>


Update the view:

from django.shortcuts import render

def home(request):
    return render(request, 'home.html')

🗃️ 8. Create First Model

myapp/models.py:

from django.db import models

class Product(models.Model):
    name = models.CharField(max_length=200)
    price = models.DecimalField(max_digits=10, decimal_places=2)

    def __str__(self):
        return self.name

🔧 9. Make Migrations & Apply
python manage.py makemigrations
python manage.py migrate

🖼 10. Install Pillow (needed for ImageField)
pip install pillow


Example image model:

class Profile(models.Model):
    name = models.CharField(max_length=100)
    avatar = models.ImageField(upload_to='avatars/')

📬 11. Create First Form

myapp/forms.py:

from django import forms

class ContactForm(forms.Form):
    name = forms.CharField(max_length=100)
    email = forms.EmailField()
    message = forms.CharField(widget=forms.Textarea)


Use form in a view (views.py):

from django.shortcuts import render
from .forms import ContactForm

def contact(request):
    form = ContactForm()
    return render(request, 'contact.html', {'form': form})


Template contact.html:

<form method="post">
    {% csrf_token %}
    {{ form.as_p }}
    <button type="submit">Send</button>
</form>


Add URL:

path('contact/', views.contact, name='contact')

▶️ 12. Run the Server
python manage.py runserver


Visit:
http://127.0.0.1:8000/

✅ Summary of Useful Commands
Environment
python -m venv venv
source venv/bin/activate

Django
pip install django
django-admin startproject myproject
python manage.py startapp myapp
python manage.py runserver

Database
python manage.py makemigrations
python manage.py migrate

Extra
pip install pillow
