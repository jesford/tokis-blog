## Notes

I'm following the Django Girls [tutorial](https://www.gitbook.com/book/djangogirls/djangogirls-tutorial/details),
and working in this directory: `~/djangogirls/`

They recommend using a virtual environment for every website project. I'll use 
conda environments instead; I created one called djangotutorial: 
`$ source activate djangotutorial`

Create the directories and files for a new django site:
`$ django-admin startproject mysite .`

A few edits to `settings.py` following the [instructions](http://tutorial.djangogirls.org/en/django_start_project/), 
and then:
```
$ python manage.py migrate
$ python manage.py runserver
```
The website is now running locally here: http://127.0.0.1:8000/

Create an application (and a new blog subdirectory):
`$ python manage.py startapp blog`

Tell Django to use the `blog` app, by adding it to `settings.py`, and add a 
bunch of actual content to `blog/models.py` as outlined [here](http://tutorial.djangogirls.org/en/django_models/). Then tell Django 
that a new/updated model exists, and apply it to the database:
```
$ python manage.py makemigrations blog
$ python manage.py migrate blog
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
"Consoles" page, select option to start a bash console. Clone the GitHub
repository for the blog.

The PythonAnywhere bash console won't let me install MiniConda, so I'll use
virtual environments here, mimicking what I did with conda environments locally.
In the `~tokis-blog/` directory in the PythonAnywhere console:
```
$ virtualenv --python=python3.5 djangotutorial
$ source djangotutorial/bin/activate
$ pip install django~=1.9.5
```

The PythonAnywhere server will use a different database than I did locally. So
have to initialize it and create the log-ins there as well:
```
$ python manage.py migrate
$ python manage.py createsuperuser
```

Go to PythonAnywhere Console -> Web tab -> Add a new web app. Confirm domain
name, choose manual configuration, Python 3.5, and click Next. On the 
Configuration page, enter path to virtual environment (in this case `/home/tokiwartooth/tokis-blog/djangotutorial`). Click on the link for
`WSGI configuration file`, and replace all contents of this file with the code 
given [here](http://tutorial.djangogirls.org/en/deploy/). Save and go back to 
the Web tab. 

Click green Reload button, and a link is generated to the live
website!... which doesn't contain the blog posts created locally even though I
created an identical superuser on PythonAnwhere. (I *think* this is the expected 
behavior, because my local database containing the posts was not pushed to 
GitHub. Hopefully there will be a way to connect my local database with the one
on PythonAnywhere, or what was the point of making posts locally??)

Working locally now, edit `mysite/urls.py`, so that a new regex expression in 
`urlpatterns`, `url(r'', include('blog.urls'))`, will make the blog homepage 
(http://127.0.0.1:8000/) correspond to the list of blog entries (the page for 
which has yet to be created). Create the `blogs/urls.py` file (which the 
previous file is trying to import), and add the code given [here](http://tutorial.djangogirls.org/en/django_urls/), which assigns a view 
called `post_list` to the homepage. 

Now we need to create that view. In `mysite/views.py`, define a function called 
`post_list`, which returns a rendering of the template `post_list.html`. Create 
this file in the new project subdirectory: `blog/templates/blog/`. Add some
basic html to `blog/templates/blog/post_list.html`. Commit and push to GitHub, 
pull changes down to PythonAnywhere, and hit reload on their Web tab.

Locally, in `~/djangogirls/` type `python manage.py shell` to get an interactive
Python + Django prompt. Then enter:
```
>>> from blog.models import Post
>>> Post.objects.all()
```
The posts we created via the admin interface are listed. We can also create
posts here on the command line.
```
>>> from django.contrib.auth.models import User
>>> User.objects.all()
>>> pup = User.objects.get(username='toki')  # create an instance of user Toki
>>> Post.objects.create(author=pup, title="Pet me", text="Or I'll bite you.")
>>> Post.objects.all()  # now shows a longer list of posts
>>> post = Post.objects.get(title="What is egg?")
>>> post.publish()  # publish a previously unpublished post
```
As outlined on [this page](http://tutorial.djangogirls.org/en/django_orm/) you 
can query, filter, and publish posts from this command line. Use `exit()` when
finished.

To actually connect the database of models to the template, we edit 
`blog/views.py`, to render the imported posts, ordered by published date. In 
`post_list.html` we include Django code, as given [here](http://tutorial.djangogirls.org/en/django_templates/). A for loop in 
Django looks something like 
```
{% for post in posts %}
    {{ post }}
{% endfor %}
```
Finish copying the Django html linked above. Push to GitHub (including the 
database, which I removed from `.gitignore`), pull down to PythonAnywhere, and
reload.

Left off tutorial at top of [this page](http://tutorial.djangogirls.org/en/css/).
