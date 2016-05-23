## Notes

I'm following the django girls [tutorial](https://www.gitbook.com/book/djangogirls/djangogirls-tutorial/details),
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

Left off tutorial at top of [this page](http://tutorial.djangogirls.org/en/django_admin/).
