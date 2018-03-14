# Backend Conceptual Warmup

## Instructions

- Fork and clone this repository
- Place your answers inside of this file (you can keep these answers to a sentence or two)
- Submit a pull request to submit the assignment

## Questions

1. What is Jinja2 used for?
Jinja2 is a templating system used with Python for web development


2. What is a migration? What is the purpose of a migration?
Migration is used to change the schema of the database table without directly accessing it. Like adding or remvoing new columns, changing data types or restrictions.


3. What is a model?
Model is a representation of the database table in the backend file, including the column name, data type and other constraints. Also, includes the primary and foriegn key relations.


4. What is a route or endpoint?
Endpoint is the part or url after the first slash. Like '/users' or '/users/new'


5. What is the difference between GET and POST?
GET request is idempotent, while POST request is not. GET request never changes the result, POST request gives different result. POST is generally used to add information to database, while GET retrives information.


5. How would you explain what RESTful routing is?
Standardization of how you define routes starting with root '/', and bulding further with '/<thing name>', '/<thing name>/new', '/<thing name>/id', '/<thing name>/id/edit'


6. What is SQL?
SQL is called Standard Query Language, which is used for interacting with the database, like updating, deleting, retriving information.


7. What is a relational database?
A relational database has rows and columns. All entries have same column information, which may or may not be null. It has primary keys to keep each record unique.


8. How would you explain what a redirect is?
A redirect is a request which a server points to another endpoint or another type of request. Redirect is actually 2 sets of requests, where the client sends a new GET reguest to server to which it gets redirected.


9. What is the difference between `redirect` and `render_template`? When would you use one or the other?
Redirect points client to different endpoint or different tpe of request than original. Render Template does not redirect, but loads the page with GET request.


- What does the following code do?

```py
student = Student('Joel', 'Burton')
db.session.add(student)
db.session.commit(student)
```
Creates a new instance of student class and adds a new student record to database


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
If the client sends a GET request, then it sends the index page for loading to the web browser along with all the students' information.
If the client sends a POST request, then the student record gets loaded into the database and then redirected back to the GET request listed above.


- What does the following code do?

```sh
flask db init
```
Initialzes the flask db migrations and creates the migrations directory to keep track of DDL changes.


- What does the following code do?

```sh
flask db migrate -m "adding favorite_color column to students table"
```
Creates a new migrations file with recent DDL changes, as per the message we are addinf a new column called favorite_color to students table.


- What does the following code do?

```sh
flask db upgrade
```
Applies the changes in the most recent migrations file to the database. In other words upgrade the database to the newwest version.


- Given the resource `students` - write out all 7 RESTful routes (include the HTTP verb and endpoint)
'/' - GET - root view function
'/students' - GET, POST - index view function
'/students/new' - GET - new view function
'/students/<id>/' - GET, PATCH, DELETE - show view function
'/students/<id>/edit' - GET - edit view function


- Imagine we want to add another resource for `excuses` which is a 1 to Many with `students` - write out all 7 RESTful routes that nest excuses inside of students (include the HTTP verb and endpoint)

'/students/<id>/excuses' - GET, POST - excuses_index view function
'/students/<id>/excuses/new' - GET - excuses_new view function
'/students/<id>/excuses<id>/' - GET, PATCH, DELETE - excuses_show view function
'/students/<id>/excuses<id>/edit' - GET - excuses_edit view function


