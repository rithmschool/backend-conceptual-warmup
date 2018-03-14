# Backend Conceptual Warmup

## Instructions

- Fork and clone this repository
- Place your answers inside of this file (you can keep these answers to a sentence or two)
- Submit a pull request to submit the assignment

## Questions

1. What is Jinja2 used for?

Jinja is a template language tool used with the Flask framework to integrate python data
into HTML pages.

2. What is a migration? What is the purpose of a migration?

A migration is an update/change to a database. It's purpose is to effectively
keep track on what changes have been made in a 'Git' style fasion.

3. What is a model?

A model is a like a blueprint layout for how data should be laid out
in a database using sqlalchemy. It inherits from the sqlalchemy Model meta class.

4. What is a route or endpoint?

A route/endpoint is a url used with a browser to show specific information via
HTTP requests.

5. What is the difference between GET and POST?

GET is idempotent and is used to retreive information. It's also slightly faster than POST.

POST is primarily used for sending information back to a server in secure fasion; this
typically comes after a form has been used/submitted.

5. How would you explain what RESTful routing is?

RESTful routing is a convention that aims to have websites designed to a standard.
The aim is to have any developer jump into a project and understand what area of a
resource contains or works with certain information.

6. What is SQL?

SQL is a database management tool.

7. What is a relational database?

A relational database involves multiples tables connected to each other; ie users and messages

8. How would you explain what a redirect is?

A redirect involves 2 cycles between the client and server ***need to work on this definition
...in which the client has request for certain information

9. What is the difference between `redirect` and `render_template`? When would you use one or the other?

render_template is used primarly for GET requests and involves simply generating an HTML page with the relevant python information.


redirect is used for sending information back to the server with information that can
be considered when handling non-GET requests.


- What does the following code do?

```py
student = Student('Joel', 'Burton')
db.session.add(student)
db.session.commit(student)
```

A Student model with the values 'Joel' and 'Burton' is assigned to the variable 'student'.
A session is started that is required for modifying a database. Here the contents within
student is added to a database and then saved via commit.


- What does the following code do?

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

The decrorator @app.route('/students', methods=["GET", "POST"]) is used with the view
function index(). When this route is just access/read, a "GET" request is used to
render index.html with a collection of students. When a "POST" request is made,
via a form, a new student is created and add to the database. Afterwards, a redirect
is used to go back to the index view function with a GET request to generate the
index.html page that may have all the students including the new student.

- What does the following code do?

```sh
flask db init
```

The creates an 'alembic' table that is used for tracking..? 'flask db migrate'
can then be used to create tables and make a modifications. A migration folder is added
to the project that can be later referred for viewing modifications.

- What does the following code do?

```sh
flask db migrate -m "adding favorite_color column to students table"
```

This stages the changes for a database to have which should be reflected from the message.
A file is genrated in the versions folder within the migrations folder that reflects the changes that will be made/updated to show in the in area with the upgrade.  Information before the change can also be viewed in the area of the versions file that has 'downgrade'

- What does the following code do?

```sh
flask db upgrade
```

The soldifies the changes and updates the changes within the database

- Given the resource `students` - write out all 7 RESTful routes (include the HTTP verb and endpoint)

*CRUD (create read update delete considered below)

GET '/students' -> index.html reading all students

GET '/students/new -> new.html show form for creating a new student

GET '/students/<id>' -> show.html show the information for a student matching id in database

GET '/students/<id>/edit' -> edit.html show the page to edit a student

POST '/students/new' -> new.html create new student

PATCH '/students/<id>/edit' -> edit.html edit a student's info

DELETE '/students/<id>/edit' -> edit.html delete a student


- Imagine we want to add another resource for `excuses` which is a 1 to Many with `students` - write out all 7 RESTful routes that nest excuses inside of students (include the HTTP verb and endpoint)

**html files in excuses folder

GET '/students/<id>/excuses' -> index.html reading all excuses associated with a student

GET '/students/<id>/excuses/new' -> new.html show form for creating a new excuse for a student

GET '/students/<id>/excuses/<excuse_id>' -> show.html show the information for an excuse

GET '/students/<id>/excuses/<excuse_id>/edit' -> edit.html show the page to edit an excuse

POST '/students/<id>/excuses/new' -> new.html create new excuse

PATCH '/students/<id>/excuses/<excuse_id>' -> edit.html edit an excuse

DELETE '/students/<id>/excuses/<excuse_id>' -> edit.html delete a excuse



