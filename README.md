<h1>
🚀 1. Installation & Environment Setup
</h1>

<h3>
1. Create & Activate Virtual Environment
</h3>

# Create virtual environment
python -m venv venv

# Activate (Windows)
venv\Scripts\activate

# Activate (Mac/Linux)
source venv/bin/activate

<h3>
📦 2. Install Django
</h3>

pip install django


Verify installation:

django-admin --version

<h3>
🏗️ 3. Create First Django Project
</h3>

django-admin startproject myproject


Move into the project:

cd myproject


Run the server to test:

python manage.py runserver

<h3>
🧩 4. Create First App
</h3>

python manage.py startapp myapp


Add the app to settings.py:

INSTALLED_APPS = [
    ...
    'myapp',
]

<h3>
🌐 5. Create First URL
</h3>

Project-level URL (myproject/urls.py):
from django.contrib import admin
from django.urls import path
from myapp import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', views.home, name='home'),
]


<h3>👁️ 6. Create First View (myapp/views.py)</h3>

from django.http import HttpResponse

def home(request):
    return HttpResponse("Hello, Django!")

<h3>📄 7. Create First HTML Template (Optional)</h3>

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

<h3>
🗃️ 8. Create First Model
</h3>

myapp/models.py:

from django.db import models

class Product(models.Model):
    name = models.CharField(max_length=200)
    price = models.DecimalField(max_digits=10, decimal_places=2)

    def __str__(self):
        return self.name

<h3>
🔧 9. Make Migrations & Apply
</h3>
python manage.py makemigrations
python manage.py migrate

<h3>
🖼 10. Install Pillow (needed for ImageField)
</h3>
pip install pillow


Example image model:

class Profile(models.Model):
    name = models.CharField(max_length=100)
    avatar = models.ImageField(upload_to='avatars/')


<h3>
📬 11. Create First Form
</h3>

myapp/forms.py:

from django import forms

`````class ContactForm(forms.Form):
    `````name = forms.CharField(max_length=100)
    `````email = forms.EmailField()
    `````message = forms.CharField(widget=forms.Textarea)


Use form in a view (views.py):

from django.shortcuts import render
from .forms import ContactForm

`````def contact(request):
    `````form = ContactForm()
    `````return render(request, 'contact.html', {'form': form})


Template contact.html:

<form method="post">
    {% csrf_token %}
    {{ form.as_p }}
    <button type="submit">Send</button>
</form>


Add URL:

path('contact/', views.contact, name='contact')

<h3>
▶️ 12. Run the Server
</h3>
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
