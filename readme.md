# Backend Conceptual Warmup

## Instructions

* Fork and clone this repository
* Place your answers inside of this file (you can keep these answers to a sentence or two)
* Submit a pull request to submit the assignment

## Questions

1.  What is Jinja2 used for?
    Jinja is used as a front-end templating language to render html pages which will be served from a Flask backend. Jinja allows for additional functionality like inheritence and programming logic to be used in the html view.
2.  What is a migration? What is the purpose of a migration?
    A migration is technique for updating database tables and columns (ddl changes) programmaticly. Migrations allow for the table/column schema to be shared among many people and to easily revert to previous schemas with minimal destruction of data.
3.  What is a model?
    A model is a programmatic representation of a database. In python, we would 'model' our data by making a class that contains the schema (ddl) that we want a table in our database to look like.
4.  What is a route or endpoint?
    A route/endpoint is the last part of the url, after the domain has been specified. Many different endpoints can exist on the same domain, each of which can be handled by the backend in different ways.
5.  What is the difference between GET and POST?
    GET requests are used for viewing data. Get requests are idempotent -- they do not change the data that they are acting upon. Information can be send in a get request via a query string, but data sent in a query string is public and be limited in scope. POST requests send data to the server. They are private and contain data in a 'body' section, which can contain large amounts of information.
6.  How would you explain what RESTful routing is?
    Restful routing is a set of standards and conventions for how routing should be performed. Restful routing has standard endpoints (/, /datas, /datas/new, /datas/<id>, /datas/<id>/edit)
7.  What is SQL?
    SQL - structured query language. SQL is a very popular query language for interacting with relational databases.
8.  What is a relational database?
    A relational database is a database that has it's data structured in a specific way (tables, columns, rows). Importantly, tables can be connected to other tables in a variety of different ways.
9.  How would you explain what a redirect is?
    A redirect is a way send control to a different route (and different route handling via function) from within backend code. Importantly, the redirect sends a 'location' data field back to the client, which instructs the client to make a request to the location (endpoint) specified.
10. What is the difference between `redirect` and `render_template`? When would you use one or the other?
    render_template is used to render a templated html page and serve that html page to the client.
    redirect sends a location (another endpoint) back to the client, and instructs the client to send another request to that endpoint

* What does the following code do?

```py
student = Student('Joel', 'Burton')
db.session.add(student)
db.session.commit(student)
```

##creates a student object with the properties of 'Joel' and 'Burton' and adds it a database
##NOTE: This presupposes configuration and a bunch of other stuff has been done correctly

* What does the following code do?

```py
@app.route('/students', methods=["GET", "POST"])
def index():
   if request.method == "POST":
       student = Student('Joel', 'Burton')
       db.session.add(student)
       db.session.commit(student)
       return redirect(url_for("index"))
   return render_template("index.html", students=Student.query.all())
```

##Handles both get and post requests to the /students endpoint
##if the request is POST, creates a student object with hardcoded data and adds to database, then redirects
##back to the index view function (after the client recieves the redirect, it will send a GET request to the '/students' endpoint)
##if the request is GET, the view function renders an html page "index.html" and serves it to the client
##NOTE: we can assume that index.html is written in a templating engine because we also pass data to the html page

* What does the following code do?

```sh
flask db init
```

##initializes our project for migrations (creates migrations folder, adds a bunch of stuff to that folder, etc)
##it's important to note that this command only needs to be run once

* What does the following code do?

```sh
flask db migrate -m "adding favorite_color column to students table"
```

##creates a new migration
##this will look at our models in app.py or a separate folder and make a migration to reflect the schema
##we define there
##it's important to note that no actual changes occur to our database in this stage

* What does the following code do?

```sh
flask db upgrade
```

## make DDL changes to our connected SQL database to reflect our most recent migration

* Given the resource `students` - write out all 7 RESTful routes (include the HTTP verb and endpoint)

##ANSWER
GET /students
GET /students/new
GET /students/<id>
GET /students/<id>/edit
POST /students
PATCH /students/<id>
DELETE /students/<id>
##END ANSWER

* Imagine we want to add another resource for `excuses` which is a 1 to Many with `students` - write out all 7 RESTful routes that nest excuses inside of students (include the HTTP verb and endpoint)

##ANSWER
GET /students/<student_id>/excuses
GET /students/<student_id>/excuses/new
GET /students/<student_id>/excuses/<excuse_id>
GET /students/<student_id>/excuses/edit
POST /students/<student_id>/excuses
PATCH /students/<student_id>/excuses/<excuse_id>
DELETE /students/<student_id>/excuses/<excuse_id>
##END ANSWER
