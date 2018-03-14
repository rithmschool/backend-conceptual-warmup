# Backend Conceptual Warmup

## Instructions

* Fork and clone this repository
* Place your answers inside of this file (you can keep these answers to a sentence or two)
* Submit a pull request to submit the assignment

## Questions

1.  What is Jinja2 used for?
    Jinja2 is used to templating in flask apps with python and html
2.  What is a migration? What is the purpose of a migration?
    A migration is used to updating a database and keeping track of the version control.
3.  What is a model?
    A model is a certain type of resource. For example the Student model is used to create the student resource
4.  What is a route or endpoint?
    A route or endpoint is the destination
5.  What is the difference between GET and POST?
    GET is used to request information
    POST is used to send information and
6.  How would you explain what RESTful routing is?
    RESTful routing is an easy readable way to layout a CRUD website.
7.  What is SQL?
    SQL is a programming language used for databases.
8.  What is a relational database?
    A relational database is when two tables in the database are linked to each other in someway.
9.  How would you explain what a redirect is?
    A redirect is sending an user to a specific route
10. What is the difference between `redirect` and `render_template`?
    A redirect is sending an user to a specific route function
    a render_template simply displays a specific template
    When would you use one or the other?
    I would use redirect when I want to run more python code than just rendering a template

* What does the following code do?

```py
student = Student('Joel', 'Burton')
db.session.add(student)
db.session.commit(student)
```

This is creating a new student and adding/saving it to the database.

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

This is an index route for students on a flask app that allows for a student to be created in a database and saved, and then index.html rendered.

* What does the following code do?

```sh
flask db init
```

initializes a database

* What does the following code do?

```sh
flask db migrate -m "adding favorite_color column to students table"
```

makes a migration in a database with the message"adding favorite_color column to students table"

* What does the following code do?

```sh
flask db upgrade
```

updgrade and saves a database

* Given the resource `students` - write out all 7 RESTful routes (include the HTTP verb and endpoint)

GET /students
GET /students/new
POST /students/create
PATCH /students/id/edit
GET /students/show
GET /students
DELETE /students/id

* Imagine we want to add another resource for `excuses` which is a 1 to Many with `students` - write out all 7 RESTful routes that nest excuses inside of students (include the HTTP verb and endpoint)
