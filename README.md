# Flask SQLAlchemy (with Examples)

[page location](https://pythonbasics.org/flask-sqlalchemy/)

The example code does not work due to the latest Flask version.  My solution was to add the code to a package 'web'.

## Install the flask-sqlalchemy extension

```bash
% pip install flask-sqlalchemy
```

## Import the SQLAlchemy class from the extension

Inside the __init__.py file...

```bash
from flask_sqlalchemy import SQLAlchemy
```

define a method 'create_app' and inside:

- create instance of Flask 'app'
- Configure the secret_key
- configure database path
- Initialize db

```bash
    app = Flask(__name__)
    app.secret_key = 'SECRET_KEY'
    app.config["SQLALCHEMY_DATABASE_URI"] = 'sqlite:///students.sqlite3'
    db.init_app(app)
```

## Define models of class SQLAlchemy

## Add the views

- Add show_all.html
- Add new.html

## Define app context

```bash
    with app.app_context():
       db.create_all()
```

## Create folder 'templates'

## Create files new and show_all

