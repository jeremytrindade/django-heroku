# django-heroku
Minimal configuration to host a Django project at Heroku

## Create your virtuanenv
* virtualenv -p python3 .vEnv
* . .vEnv/bin/activate

## Installing django
* pip install django

## Create the django project
* django-admin startproject myproject
* git init to start the repository
* git add .
* git commit -m 'First commit'

## Hidding instance configuration
* pip install python-decouple
* create .env file at the root path and insert the following variables
- SECRET_KEY=Your$eCretKeyHere
- DEBUG=True

### Settings.py
* from decouple import config
* SECRET_KEY = config('SECRET_KEY')
* DEBUG = config('DEBUG', default=False, cast=bool)


## Configuring the Daba Base
* pip install dj-database-url


### Settings.py
* from dj_database_url import parse as dburl
'''
default_dburl = 'sqlite:///' + os.path.join(BASE_DIR, 'db.sqlite3')

DATABASES = {
    'default': config('DATABASE_URL', default=default_dburl, cast=dburl),
}
'''

### .env


## Static files 
pip install dj-static

### wsgi
* from dj_static import Cling
* application = Cling(get_wsgi_application())

### Settings.py
* STATIC_ROOL = os.path.join(BASE_DIR, 'staticfiles')

## Create a requirements.txt
pip freeze > requirements.txt
* Include: gunicorn and psycopg2

## Create a file Procfile and add the following code
* web: gunicorn website.wsgi --log-file -

## Create a file runtime.txt and add the following core
* python-3.5.0

## Creating the app at Heroku
* heroku apps:create app-name

### Sending configs from .env to Heroku ( You have to be inside tha folther where .env files is)
* heroku config:push

### To show heroku configs do
* heroku config 

## Publishing the app
* Create the git ignore
.idea ( see the name for you IDE)
*.sqlite3 (If you are using sqlite3)
.vEnv (Name of your virtuan env)
*pyc 

* git add .
* git commit -m 'Configuring the app'
* git push heroku master --force

## Setting the allower hosts
* include your address at the ALLOWED_HOSTS directives in settings.py

## EXTRAS
### You may need to disable the collectstatic
* heroku config:set DISABLE_COLLECTSTATIC=1

### Changing a specific configuration
* heroku config:set DEBUG=True