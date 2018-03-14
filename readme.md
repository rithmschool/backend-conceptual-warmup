# Backend Conceptual Warmup

## Instructions

* Fork and clone this repository
* Place your answers inside of this file (you can keep these answers to a sentence or two)
* Submit a pull request to submit the assignment

## Questions

* first bullets are answers added during warmup
* second bullets are answers added during discussion

1.  What is Jinja2 used for?

* incorporating python code in an html file--conditional statements and iterations can be evaluated as can database information be referenced to display

* server side templating engine

2.  What is a migration? What is the purpose of a migration?

* a migration is the creation of a system of files which monitor the state of an app file, displaying its changes to be implemented as well as what a reversion from those changes would look like; a user can then upgrade or downgrade between those file states accordingly.

* dependent on ORM (Flask Alchemy uses olyembic)

3.  What is a model?

* a model helps create the data structure of a table, Ex: the DDL with respect to creating a table's columns

* not schema, but a class
* python representation of our tables
* typically one model per table
* informs the database how

4.  What is a route or endpoint?

* the final destination of a URL where information can be processed and/or displayed accordingly

* determines how server responds to requests

5.  What is the difference between GET and POST?

* GET is a request to view information and is idempotent; this information requested is visible in the query string.
* POST is a request to add information to a server or database

* GET renders a template, does not change information and gives the same result every time as key value pairs
* POST redirects and is not idempotent, more secure as information is sent in the body of the request vs query string

5.  How would you explain what RESTful routing is?

* a convention for naming routes based off of resources which allows all developers to understand the mapping of a project without themseleves creating the routes

6.  What is SQL?

* a programming language often used for managing relational databases

* structured query language

7.  What is a relational database?

* a database which emphasizes the relation of data between tables
* a relational database is often chosen when communication between tables is important for accessing and modifying information

* database made of rows and columns

8.  How would you explain what a redirect is?

* a redirect is a possible option when returning a view function
* it will send a user from that view function's endpoint to another endpoint, or even the same endpoint to be processed with a different method

* following a non-idempotent request to the server, a response location header and value is returned, and the server generates a GET request to the location

9.  What is the difference between `redirect` and `render_template`? When would you use one or the other?

* a redirect is used to send a user to a different endpoint, or to the same endpoint to be processed as a GET request and is most often used following a POST, PUT, PATCH, or DELETE request
* render_template displays for the user a new html file and is used after processing a GET request

* redirect is 2 repsonses
* render is 1 response
* this assumes an initial successful idempotent request, the web is stateless

- What does the following code do?

```py
student = Student('Joel', 'Burton') # creates a new instance of the Student class with the arguments 'Joel' and 'Burton'
# stores this instance in the variable student
db.session.add(student) # processes that information according to the structure of the a table in a database, but does not write it
db.session.commit(student) # writes the staged information to the database

# .add opens a transaction
# .commit writes and closes that transaction
```

* What does the following code do?

```py
@app.route('/students', methods=["GET", "POST"]) # designates the endpoint and request methods accepted at that endpoint
def index(): # declares a view function called index
   if request.method == "POST": # conditional statement to process incoming POST requests
       student = Student('Joel', 'Burton') # creates a new istance of Student
       db.session.add(student) # stages the new student to be written to the database
       db.session.commit(student) # writes the staged information
       return redirect(url_for("index")) # sends the user to this same endpoint via a url_for the view function index to be processed as a GET request
   return render_template("index.html", students=Student.query.all()) # default return if receiving a GET request, generates an html page which has access to all 'students', displayed via jinja2
```

* What does the following code do?

```sh
flask db init # creates the files associated with migrations, a version control for app files when interacting with a database
```

* What does the following code do?

```sh
flask db migrate -m "adding favorite_color column to students table"
# stages the current state of an app file's commands for managing a database as well as commands to revert (flask db downgrade) to the database's current layout if the changes are written to it (via flask db upgrade)

# migration
```

* What does the following code do?

```sh
flask db upgrade # writes the changes proposed in the latest migrations versions py file; this upgrade will have an associated downgrade and reference numbers
```

* Given the resource `students` - write out all 7 RESTful routes (include the HTTP verb and endpoint)

```py
/students # GET (render_template) and POST (redirect)
/students/new # GET (render_template)
/students/<id>/edit # GET (render_template)
/students/<id> # GET (render_template), PATCH/PUT (redirect), DELETE (redirect)
```

GET /students
POST /students
GET /students/new
GET /students/<int:id>/edit
GET /students/<int:id>
PATCH /students/<int:id>
DELETE /students/<int:id>

* Imagine we want to add another resource for `excuses` which is a 1 to Many with `students` - write out all 7 RESTful routes that nest excuses inside of students (include the HTTP verb and endpoint)

```py
/students # GET (render_template) and POST (redirect)
/students/<id>/excuses # GET (render_template) and POST (redirect)
/students/new # GET (render_template)
/students/<id>/edit # GET (render_template)
/students/<id>/excuses/edit # GET (render_template)
/students/<id> # GET (render_template), PATCH/PUT (redirect), DELETE (redirect)
/students/<id>/excuses/<e_id> # GET (render_template), PATCH/PUT (redirect), DELETE (redirect)
```

GET /students/<int:id>/excuses
POST /students/<int:id>/excuses
GET /students/<int:id>/excuses/new
GET /students/<int:id>/excuses/<int:e_id>/edit
GET /students/<int:id>/excuses/<int:e_id>
PATCH /students/<int:id>/excuses/<int:e_id>
DELETE /students/<int:id>/excuses/<int:e_id>
