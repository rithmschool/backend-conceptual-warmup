# Backend Conceptual Warmup

## Instructions

* Fork and clone this repository
* Place your answers inside of this file (you can keep these answers to a sentence or two)
* Submit a pull request to submit the assignment

## Questions

1.  What is Jinja2 used for?
    <!-- templating -> can evaluate variables and python code in HTML files -->
2.  What is a migration? What is the purpose of a migration?
    <!-- to keep track of changes to the db, ddl specifically -->
3.  What is a model?
    <!-- like a class, defines the information to be kept in a db table -->
4.  What is a route or endpoint?
    <!-- corresponds to the location on the file system you want to load (in the url)-->
5.  What is the difference between GET and POST?
    <!-- GET is idempotent, POST is not, GET grabs information from the server, POST can make changes to information on the server -->
6.  How would you explain what RESTful routing is?
    <!-- a convention by which resources, the functions associated with displaying their information, and their routes are organized -->
7.  What is SQL?
    <!-- a language for manipulating relational dbs -->
8.  What is a relational database?
    <!-- a db where information in tables corresponds to information in other tables -->
9.  How would you explain what a redirect is?
    <!-- a redirect makes a request to an endpoint based on the function name passed in -> make a request, get a response, make another request, get another response -->
10. What is the difference between `redirect` and `render_template`? When would you use one or the other?
    <!-- redirect makes a get request to an endpoint based on function name, multiple transactions, render_template displays the file associated passed into it -->

* What does the following code do?

```py
student = Student('Joel', 'Burton')
db.session.add(student)
db.session.commit(student)
```

<!-- adds a row in the student table with the information Joel Burton -->

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

<!-- define the index function. if you submit a get request, index.html is rendered and the students variable passed in, for a post request, the student information is added to the db and you're redirected to the function with a get request -->

* What does the following code do?

```sh
flask db init
```

<!-- like git init, starts keeping track of db migrations -->

* What does the following code do?

```sh
flask db migrate -m "adding favorite_color column to students table"
```

<!-- creates a migration, no changes commited to the server yet, a new migration version file is created -->

* What does the following code do?

```sh
flask db upgrade
```

<!-- commits the migration, check version file first to see if you're cool with the upgrade/downgrade-->

* Given the resource `students` - write out all 7 RESTful routes (include the HTTP verb and endpoint)
  <!-- /students - GET -->
  <!-- /students - POST -->
  <!-- /students/new GET -->
  <!-- /students/<int:id>/edit - GET -->
  <!-- /students/<int:id> - GET -->
  <!-- /students/<int:id> - PATCH -->
  <!-- /students/<int:id> - DELETE -->
* Imagine we want to add another resource for `excuses` which is a 1 to Many with `students` - write out all 7 RESTful routes that nest excuses inside of students (include the HTTP verb and endpoint)
  <!-- /students/<int:student_id>/excuses - GET -->
  <!-- /students/<int:student_id>/excuses - POST -->
  <!-- /students/<int:student_id>/excuses/new GET -->
  <!-- /students/<int:student_id>/excuses/<int:excuse_id>/edit - GET -->
  <!-- /students/<int:student_id>/excuses/<int:excuse_id> - GET -->
  <!-- /students/<int:student_id>/excuses/<int:excuse_id> - PATCH -->
  <!-- /students/<int:student_id>/excuses/<int:excuse_id> - DELETE -->
