# Backend Conceptual Warmup

## Instructions

- Fork and clone this repository
- Place your answers inside of this file (you can keep these answers to a sentence or two)
- Submit a pull request to submit the assignment

## Questions

1. What is Jinja2 used for?
Jinja2 evaluates and executes python code inside an html file and updates the file accordingly 
2. What is a migration? What is the purpose of a migration?
A migration is a file reflecting a schema change to the database.  It enables all developers to be up to date with the changes, as well as downgrade to a previous state.
3. What is a model?
A model is a python class that gets mapped to a SQL table
4. What is a route or endpoint?
A route or endpoint is the path appearing in the URL sent with an http request to a server
5. What is the difference between GET and POST?
A GET request is idempotent; a POST request is not.  The former just looks at data; the latter may alter data on the server.
5. How would you explain what RESTful routing is?
RESTful routing is a convention for naming paths and structuring web applications.
6. What is SQL?
SQL is a language for managing a relational database.  It's been around since the '70s.
7. What is a relational database?
A relational database is one where tables are interconnected (related) to each other.  That is, columns in one table can refer to data in another table.
8. How would you explain what a redirect is?
A redirect is involves two requests from a client and two responses from a server.  The client requests one path, the server responds with a new location, the client requests that new path, the server responds for that path.
9. What is the difference between `redirect` and `render_template`? When would you use one or the other?
The first involves two requests and two responses, redirecting the client to a different path.  The latter involves only one request and one response.  A redirect is used after executing a request that is not idempotent.  A render_template is for an idempotent GET request.

- What does the following code do?

```py
student = Student('Joel', 'Burton')
db.session.add(student)
db.session.commit(student)
```
This code instantiates an instance of the Student class, then uses the ORM to map data to a table, adding a row with this student's data.

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
This code handle GET and POST requests differently for the path /students.  For a POST, it creates an instance of the student class, then adds that students data to the students table in the database via the ORM, then redirects to the index page.  For a GET, it sends the html file for the index page, populated with the data for all students.

- What does the following code do?

```sh
flask db init
```
This code initializes flask migrate so that migration files can be created and then committed to the database.

- What does the following code do?

```sh
flask db migrate -m "adding favorite_color column to students table"
```
This code creates a migration file reflecting schema changes to the database.  An optional message is included describing the change.

- What does the following code do?

```sh
flask db upgrade
```
This code executes SQL code to make schema changes to the database described in the migration file.

- Given the resource `students` - write out all 7 RESTful routes (include the HTTP verb and endpoint)
1 - /students               GET
2 - /students/new           GET
3 - /students               POST
4 - /students/<int:id>/edit GET
5 - /students/<int:id>      GET
6 - /students/<int:id>      PATCH
7 - /students/<int:id>      DELETE

- Imagine we want to add another resource for `excuses` which is a 1 to Many with `students` - write out all 7 RESTful routes that nest excuses inside of students (include the HTTP verb and endpoint)
1 - /students/<int:id>/excuses                      GET
2 - /students/<int:id>/excuses/new                  GET
3 - /students/<int:id>/excuses                      POST
4 - /students/<int:id>/excuses/<int:msg_id>/edit    GET
5 - /students/<int:id>/excuses/<int:msg_id>         GET
6 - /students/<int:id>/excuses/<int:msg_id>         PATCH
7 - /students/<int:id>/excuses/<int:msg_id>         DELETE



