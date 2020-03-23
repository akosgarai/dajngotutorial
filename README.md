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

Now we have the empty db.
