# Flask SQLAlchemy (with Examples)

[page location](https://pythonbasics.org/flask-sqlalchemy/)

The example code does not work due to the latest Flask version changes.  My solution was to add the code to a package 'web'.  The app.py file calls the __init__.py inside the package and that allows the sqlite database to work fine.

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

As seen below sqlalchemy allows us to abstract the handling of the database be it sqlite, postgres or SQL using python to execute.
When a object of the class db.Model is instantiated the __init__ method adds the attributes of name, email etc.

```bash
    class students(db.Model):
       id = db.Column('student_id', db.Integer, primary_key = True)
       name = db.Column(db.String(100))
       city = db.Column(db.String(50))
       addr = db.Column(db.String(200)) 
       pin = db.Column(db.String(10))

       def __init__(self, name, city, addr,pin):
              self.name = name
              self.city = city
              self.addr = addr
              self.pin = pin
```

## Add the views

For this example we added the views 'show_all' and 'new'.

```bash
       @app.route('/')
       def show_all():
              return render_template('show_all.html', students = students.query.all() )

       @app.route('/new', methods = ['GET', 'POST'])
       def new():
              if request.method == 'POST':
                     if not request.form['name'] or not request.form['city'] or not request.form['addr']:
                            flash('Please enter all the fields', 'error')
                     else:
                            student = students(request.form['name'], request.form['city'], request.form['addr'], request.form['pin'])
              
                            db.session.add(student)
                            db.session.commit()
                            flash('Record was successfully added')
                            return redirect(url_for('show_all'))
              return render_template('new.html')
```

## Define app context

Have define all the relevant models / tables We can now define the app context for db.create_all().  Finally we close the method 'create_app() with a return of 'app'.

```bash
    with app.app_context():
       db.create_all()
                        
    return app
```

## Create folder 'templates'

To implement the views we need to put the html files inside the 'templates' directory, adding html files new.html and show_all.html.
