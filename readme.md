# Backend Conceptual Warmup

## Instructions

- Fork and clone this repository
- Place your answers inside of this file (you can keep these answers to a sentence or two)
- Submit a pull request to submit the assignment

## Questions

1. What is Jinja2 used for?
Jinja2 is used for converting data into html strings. 
*Used for generating templates and they're being generated on the server. 
*It's used to power the server side templates. 

2. What is a migration? What is the purpose of a migration?
A migration is needed when we need to update tables/columns in our database/SQL. The purpose of it is to ensure that our SQL has all the relevant update.

3. What is a model?
A model is used when we want to create an instance of something, such as a car, snack, or user. 
*It's a class and a python representation of your tables of our server side language of choice. 
*It tells your ORM how to structure your database. 

4. What is a route or endpoint?
A route or an endpoint is where our page takes us. 
*It determines how our servers responds to requests.

5. What is the difference between GET and POST?
A GET request renders a template and displays information. A POST request requires us to update information on our page/in our server can redirect us to another page with the new information or render a template with the updated information. 
*GET is idempotent (a request that has the same response over and over again) and POST isn't. 
*Data is sent to the server via GET will be in the query string via key value pairs. 
*Data is sent to the server via POST will be sent in the body of the request. POST will be more secure. 

5. How would you explain what RESTful routing is?
RESTful routing is an order of how our endpoints and view functions are organized. RESTful routing requires us to follow a set of conventions when organizing our code (view functions) and endpoints. 
*Set of standardized rules for routing. 

6. What is SQL?
SQL is our database on the backend. 
*Structured Query Language (SQL) it's the language for relational databases. 

7. What is a relational database?
A relational database is a database that has relations/corresponds with other tables within that database. 

8. How would you explain what a redirect is?
A redirect is when you are sent to another template or html page. 

9. What is the difference between `redirect` and `render_template`? When would you use one or the other?
A redirect will send you to a different location (html) and render_template would render an html template. For GET requests, you would use render_template to display information and for other requests, such as POST, PATCH, DELETE, you would use a redirect. Or if you were going to the root (/) you would be redirected to the index.html page. 
*Redirect not idempotent. Requires two requests and two responses: POST request -> Value of Location (header) response. Browser will send back GET request to the endpoint. 
*Render_template - GET request and one response
*You always redirect when you POST/PATCH successfully. If is isn't successful, you'll want to render the form.

- What does the following code do?
The code below creates an instance of the Student model and adds the instance to our table. 
*db.session.add starts the transaction - nothing is saved to SQL yet.
*db.session.commit completes the transaction
```py
student = Student('Joel', 'Burton')
db.session.add(student)
db.session.commit(student)
```

- What does the following code do?
The code below creates a view function (index) for the endpoint (/students) and checks for two requests. If it's a POST request, it will create an instance of the Student model with the name Joel Burton and will add it to our table in SQL. If it's a GET request, it will simply render the template and display all the names of the students. 
*the function will only be run when you use either GET or POST
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

- What does the following code do?
The code below initializes the database. You only want to do this once because we'll only be using one database. Within our database however, we can work with many tables.
*This adds alembic and migrations to our folder. 
```sh
flask db init
```

- What does the following code do?
This code below migrates a change you've made the the table and creates a new file in your migrations folder. You'll want to view this file to verify that the column has been added to the students table before finalizing (upgrading) the migration. 
*This generates pending migrations and gives you an opportunity to edit. 
```sh
flask db migrate -m "adding favorite_color column to students table"
```

- What does the following code do?
After verifying that the migrations file, you can use the following code to upgrade your table in SQL. 
*Executes pending migrations. 
```sh
flask db upgrade
```

- Given the resource `students` - write out all 7 RESTful routes (include the HTTP verb and endpoint)
GET /students [show all students]
POST /students
GET /students/new [render form new student] 
GET /students/<int:id> [show student]
GET /students/<int:id>/edit [show edit page]
PATCH /students/<int:id>/edit [edit student]
DELETE /students/<int:id> [delete student]

correct:
*GET /students
*GET /students/new
*POST /students
GET /students/<int:id>
GET /students/<int:id>/edit
PATCH /students/<int:id>
DELETE /students/<int:id>/edit

- Imagine we want to add another resource for `excuses` which is a 1 to Many with `students` - write out all 7 RESTful routes that nest excuses inside of students (include the HTTP verb and endpoint)
GET /students/<int:id>/excuses [show all excuses for one student]
POST /students/<int:id>/excuses 
POST /students/<int:id>/excuses/new [add a new excuse for one student]
GET /students/<int:id>/excuses/<int:excuse_id>/show [show the individual excuse for one student]
GET /students/<int:id>/excuses/<int:exucse_id>/edit [show edit page]
PATCH /students/<int:id>/excuses/<int:excuse_id>/edit [edit the excuse for one student]
DELETE /students/int:id/excuses/<int:excuse_id> [delete the excuse for one student]

correct:
*GET /students/<int:id>/excuses
*GET /students/<int:id>/excuses/new
*POST /students/<int:id>/excuses
GET /students/<int:id>/excuses/<int:excuse_id>
GET /students/<int:id>/excuses/<int:excuse_id>/edit
PATCH /students/<int:id>/excuses/<int:excuse_id>
DELETE /students/<int:id>/excuses/<int:excuse_id>
