# Backend Conceptual Warmup

## Instructions

- Fork and clone this repository
- Place your answers inside of this file (you can keep these answers to a sentence or two)
- Submit a pull request to submit the assignment

## Questions

1. What is Jinja2 used for?
    Jinja2 is the templating module of flask. It is used to create and read in teamplates and to transfer variables between webpages.
2. What is a migration? What is the purpose of a migration?
    Migration is the manipulation of tables and columns in a database in a controled, tracable and reproducable manner. This is etremely important in teamwork projects.
3. What is a model?
    Model usually refers to a built-in class in object-oriented programming languages. User-defined classes can inherit properties / methods from the models they are based on.
4. What is a route or endpoint?
    A route or endpoint is part of the server-side handling of requests from the client-side. Sending requests to these routes render webpages, redirect, or send information to the client.
5. What is the difference between GET and POST?
    GET and POST are both request types (verbs). But while GET is idempotent (has the same effect every time the request is made), POST is used to manipulate a resource on the server-side.
5. How would you explain what RESTful routing is?
    RESTful routing is a convention of building routes or endpoints for a resource or resources on the server side. It is commonly used to build CRUD (Create, Read, Update, Delete) web applications.
6. What is SQL?
    SQL is a database programming language. This is the oldest (originates from the 70s) and most commonly used language in database programming and it is particularly adapt for use in relational databases. 
7. What is a relational database?
    A relational database is a database that has multiple tables and a schema that contains relationships (cross-references) between these tables. This organization style is well-liked for its robustness and scalability.
8. How would you explain what a redirect is?
    Redirect is a server-side response to a client request that redirects the client to another (or even the same) route or endpoint. This is usually used after POST/PATCH/DELETE request was made to the server that requires resource manipulation.
9. What is the difference between `redirect` and `render_template`? When would you use one or the other?
    Render_template renders a webpage and sends it to the client. Redirect redirects the client to another (or even the same) route or endpoint.

- What does the following code do?

```py
student = Student('Joel', 'Burton')
db.session.add(student)
db.session.commit(student)
```

This code creates a student instance of the Student class and then opens a session to that instance to the database. Finally it closes the session and commits the change to the database. 
(I'm not sure if the last line is correct; it would definitely work as db.session.commit())

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

This is the basic route of the student resource that is responsible for renderring the index.html webpage of the student resource. In addition, it is also the endpoint that handles requests to create new instances of the Student class, save them in the database, and then redirect to render the student index.html again.

- What does the following code do?

```sh
flask db init
```

This command creates the basic migration folder and files in the project folder when using the flask_migrate module. This is necessary to be able to migrate the database changes later.

- What does the following code do?

```sh
flask db migrate -m "adding favorite_color column to students table"
```

This command initiates a database migration (tracable and structurally reversable database change) and creates a version file when using the flask_migrate module. Judging by the comment added to the command, it is intended to create a new column in the students table. At this point, only the py files has been changed, but no change to the database is made. 

- What does the following code do?

```sh
flask db upgrade
```

This command makes the desired changes to the database after a database migration has been initiated when using the flask_migrate module. It calls the upgrade function in the migration version file.

- Given the resource `students` - write out all 7 RESTful routes (include the HTTP verb and endpoint)
     
     HTTP Verb   Route
    1. GET  ->  /students
    2. GET  ->  /students/new
    3. POST ->  /students
    4. GET  ->  /students/id
    5. PATCH  ->  /student/id
    6. DELETE  ->  /student/id
    7. GET  ->  /student/id/edit

- Imagine we want to add another resource for `excuses` which is a 1 to Many with `students` - write out all 7 RESTful routes that nest excuses inside of students (include the HTTP verb and endpoint)

      HTTP Verb        Route
    1. GET  ->  /students/id/excuses
    2. GET  ->  /students/id/excuses/new
    3. POST ->  /students/id/excuses
    4. GET  ->  /students/id/excuses/excuse_id
    5. PATCH  ->  /student/id/excuses/excuse_id
    6. DELETE  ->  /student/id/excuses/excuse_id
    7. GET  ->  /student/id/excuses/excuse_id/edit


