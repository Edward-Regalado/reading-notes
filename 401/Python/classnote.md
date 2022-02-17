poetry add django-environ
poetry export -f requirements.text -o
dcu --build

make sure to have .env in the .gitignore file
create a second .env in the root of your folder in addition to the one in the project file


### inside settings.py file

from pathlib import Path
import eviron

.env file needs to be in the project level folder

evn = environ.Env(
    DEBUG=(bool, False)
)

eviron.Env.read_env()

move secret key to .env file

SECRET_KEY = env.str('SECRET_KEY')

DEBUG = env.bool('DEBUG')

ALLOWED_HOST

DATABASES = {
    CHANGE NAME, USER, PASSWORD, HOST AND PORT TO .env varibles
}

### inside .env file

SECRET_KEY=8282838383...
DEBUG=0 or 1 (True or False)
ALLOWED_HOST=0.0.0.0, 127.0.0.1, localhost
DATABASE_NAME=postgres
DATABASE_USER=postgres
DATABASE_PASSWORD=postgres
DATABASE_HOST=db
DATABASE_PORT=5432