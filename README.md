# Django related documentation

I want to know how the django framework works. Due to this, i'm following [this](https://docs.djangoproject.com/en/3.0/) tutorial, to play around with this stuff.

## What have i done?

I already have python, so i don't need to setup it. Only the virtualenv is necessary to be created, so i followed the tutorial, and created it with the following command:

```bash
python3 -m venv ~/.virtualenvs/djangodev
```

I activated the environment with the following command:

```bash
source ~/.virtualenvs/djangodev/bin/activate
```

After the activation, the env name is visible in the terminal:

```bash
(djangodev) akosgarai@akos-szemetlada ~/Documents/prog/python $
```

Now i can use the python command insteead of python3. Also everything is ready to install the django:

```bash
python -m pip install Django
```

Finally let's check that the instalation was successful or not. I can try to get the version of the installed django:

```bash
python -m django --version
```

The output:

```bash
3.0.4
```

The installation was successful.

### Create project

Now everything is ready to create a new django project. I have done it with this command:

```bash
django-admin startproject djangotutorial
```

And now the initial project is ready. I can start it with the following commands:

```bash
cd djangotutorial
python manage.py runserver
```

I can check it in the browser: `http://127.0.0.1:8000/`

At this point, it would worth to make a commit, so that i have done it. Also some ignorable files and patterns were added to a gitignore file and it was committed also.

### Create application

I am in the project directory (here is the manage.py), so i can run this command to create the `polls` application:

```bash
python manage.py startapp polls
```

Let's update (based on [this](https://docs.djangoproject.com/en/3.0/intro/tutorial01/#write-your-first-view) doc) the `polls/views.py` file, create the index route. The respose is static string. After this step, I have to create the `polls/urls.py` file and add there the relevant codeblock. The last step is updating the `djangotutorial/urls.py` file, to register the new path. The app is testable in the browser (`http://127.0.0.1:8000/polls/`) after the server start command.

```bash
python manage.py runserver
```

In the meantime, i found that i have committed some `.pyc` files. It's unnecessary, so i removed them with the following command: `git rm --cached \*.pyc` and also the gitignore file was extended with them.

### Database setup

The implementation is based on [this](https://docs.djangoproject.com/en/3.0/intro/tutorial02/#database-setup) and [this](https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-django-with-postgres-nginx-and-gunicorn) tutorials.

Switch to postgres user.

```bash
sudo su - postgres
```

Create the database.

```bash
createdb djangotutorial
```

Login to db with psql command.

```bash
psql
```

Create a new user to the database.

```bash
CREATE USER djangotutorial WITH ENCRYPTED PASSWORD 'password-is-here';
```

And finally grant privileges to the user.

```bash
GRANT ALL PRIVILEGES ON DATABASE djangotutorial TO djangotutorial;
```

Now we have the empty db. Let's get some content. In the project directory, we can migrate the database.

```bash
python manage.py migrate
```

This command returned with error. I have missing dependencies. (python psycopg2, and some apt-get stuff)

```bash
sudo apt-get install libpq-dev
python -m pip install psycopg2
```

After it, the migrate command has to worked well.

```bash
python manage.py migrate
```

Now we can define some models in the `polls/models.py`. Then we have to register the polls application to our `djangotutorial/settings.py` file. The name of the application (PollsConfig) is coming from the `polls/apps.py`. Now we can create db migration files fit the following command:

```bash
python manage.py makemigrations polls
```

And the actual migration with the `migrate` command:

```bash
python manage.py migrate
```

With the django shell (`python manage.py shell`) i can define questions and choises. To make the models more readable in the shell, we can implement the `__str__` functions. The `was_published_recently` function is an example of a custom function. It returns some new questions, where the pub\_date is in one day.

### Admin interface

After creating an admin user (based on the documentation), i need to attach the polls app to the admin interface. I can do this with updating the `polls/admin.py` file.

### Views

We can create views to our application. The views needs to be attached to endpoints. We are able to display the data in django templates. To do this, we have to make a `templates` directory in the application dir. We also have to make a `polls` directory insite the newly created template dir. I can put the view templates here. We can rase 404 exceptions, and we can display error page if the content is missing (not found in the db). We can do this with shortcuts.
