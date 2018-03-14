# Backend Conceptual Warmup

## Instructions

* Fork and clone this repository
* Place your answers inside of this file (you can keep these answers to a sentence or two)
* Submit a pull request to submit the assignment

## Questions

1.  What is Jinja2 used for?
    Jinja is a template engine that is created on the server side and serves the HTML to the frontend
2.  What is a migration? What is the purpose of a migration?
    Migrations are used like git to keep track of tables and or columns added to the db. So you can update or goback to an older version
3.  What is a model?
    A model is a set of blueprints that is used to create instances of the model.
4.  What is a route or endpoint?
    An endpoint is that last part of the url before optional arguments like querystring are added denoted by ? (the last word on the leftside of the question mark)
    routes are
5.  What is the difference between GET and POST?
    GET request are used to get information/data from the db and are idempotent
    POST request are use to 'add' new data to the db
6.  How would you explain what RESTful routing is?
    Is a set of rules
7.  What is SQL?
    Structured Query Langauge is used to query a relation db
8.  What is a relational database?
    Relational db are a way to map data in association to one table to another hence conveying a relationship
9.  How would you explain what a redirect is?
    A redirect involves two request and responses from both front end and back end, it sends you to a new endpoint from another route
10. What is the difference between `redirect` and `render_template`? When would you use one or the other?
    The redirect will send you to a different route, the render_template, renders a template from the backend to front_end
    More specifically we use render_templates on GET request and redirects on POST, DELETE, PATCH/PUT

* What does the following code do?

1.  Creates an instance of a student from the Class Student
2.  we are 'adding' to a new student to the db but has yet to be finalized
3.  We are commiting a new studnet to the db

```py
student = Student('Joel', 'Burton')
db.session.add(student)
db.session.commit(student)
```

* What does the following code do?
  If method is a POST ie creating a new student, we will post new student information in the db and will be redirected to a GET reqest on index to render a template of the index.html, If the request is !POST we will just render the index.html template with all students on that page with what ever information is selected on the jinja template

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

* What does the following code do?

1.  Creates a new migration folder must have flask-migration dependency

```sh
flask db init
```

* What does the following code do?

1.  Creating a new migration, which will add a new file to the versions folder, we have created a favorite_color column students table

```sh
flask db migrate -m "adding favorite_color column to students table"
```

* What does the following code do?

1.  Assuming there are no conflicts in the migration we are updating the table to include favorite_color column

```sh
flask db upgrade
```

* Given the resource `students` - write out all 7 RESTful routes (include the HTTP verb and endpoint)

@app.route('/', methods=[GET])
def root():
return redirect(url_for('student'))

@app.route('/student', methods=[GET])
def index():
return render_template('index.html')

@app.route('/student/new', methods=[GET])
def new():
return render_template('new.html')

@app.route('/student/new', methods=[POST])
def create():
new_student = Student(info)
db.session.add(new_student)
db.seession.commit()
return redirect(url_for('index'))

@app.route('/student/<int:id>', methods=[GET])
def show(id):
findStudent = Student.query.get(id)
return render_template('show.html', student = findStudent)

@app.route('/student/<int:id>/edit', methods=[GET])
def edit(id):
findStudent = Student.query.get(id)
return render_template('edit.html', student = findStudent)

@app.route('/student/<int:id>', methods=[PATCH])
def update(id):
//get info from form send to db
return redirect('index')

@app.route('/student/<int:id>', methods=[DELTE])
def destroy(id):
//get info from form send to db
return redirect('index')

* Imagine we want to add another resource for `excuses` which is a 1 to Many with `students` - write out all 7 RESTful routes that nest excuses inside of students (include the HTTP verb and endpoint)

GET/student/<int:id>/excuses
GET/student/<int:id>/excuses/new
POST/student/<int:id>/excuses
GET/student/<int:id>/excuses/<int:message_id>/edit
GET/student/<int:id>/excuses/<int:message_id>
PATCH/student/<int:id>/excuses/<int:message_id>
DELETE/student/<int:id>/excuses/<int:message_id>
