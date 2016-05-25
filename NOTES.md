## Notes

I'm following the Django Girls [tutorial](https://www.gitbook.com/book/djangogirls/djangogirls-tutorial/details),
and working in this directory: `~/djangogirls/`

They recommend using a virtual environment for every website project. I'll use 
conda environments instead; I created one called djangotutorial: 
`source activate djangotutorial`

Create the directories and files for a new django site:
`django-admin startproject mysite .`

A few edits to `settings.py` following the [instructions](http://tutorial.djangogirls.org/en/django_start_project/), 
and then:
```
python manage.py migrate
python manage.py runserver
```
The website is now running locally here: http://127.0.0.1:8000/

Create an application (and a new blog subdirectory):
`python manage.py startapp blog`

Tell Django to use the `blog` app, by adding it to `settings.py`, and add a 
bunch of actual content to `blog/models.py` as outlined [here](http://tutorial.djangogirls.org/en/django_models/). Then tell Django 
that a new/updated model exists, and apply it to the database:
```
python manage.py makemigrations blog
python manage.py migrate blog
```

Register this new model by adding code to `blog/admin.py`, as given in 
[this page](http://tutorial.djangogirls.org/en/django_admin/). Now typing 
`python manage.py runserver` will give a log-in page here: 
http://127.0.0.1:8000/admin/

Create the superuser who can login: `python manage.py createsuperuser`, and 
enter a username, email and password. Now this user can log-in. Log-in and 
create a few blog posts...

Create a new GitHub repo for this project and push content there (aside from 
contents of `.gitignore`: listed [here](http://tutorial.djangogirls.org/en/deploy/)).

Log-in to free beginner account at https://www.pythonanywhere.com. On the 
dashboard (or "Consoles") page, select option to start a bash console. Clone the
GitHub repository for the blog.

The PythonAnywhere bash console won't let me install MiniConda, so I'll use
virtual environments here, mimicking what I did with conda environments locally.
In the PythonAnywhere console:
```
virtualenv --python=python3.5 djangotutorial
source djangotutorial/bin/activate
pip install django~=1.9.5
```

Left off tutorial at top of [this page]().
