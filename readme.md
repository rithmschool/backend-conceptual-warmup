# Backend Conceptual Warmup

## Instructions

- Fork and clone this repository
- Place your answers inside of this file (you can keep these answers to a sentence or two)
- Submit a pull request to submit the assignment

## Questions

1. What is Jinja2 used for? 
Jinja2 allows developers to write python code in our html files in order to 
render and display data that is being sent from our database.
2. What is a migration? What is the purpose of a migration ?
A migration is the process of saving prior versions of your database in order 
to keep a record of different versions of your database if you decide to switch back
to a previous version.
3. What is a model? 
A model allows us to create columns in our database based on the criteria specified
when creating our class of a particular resource. 
4. What is a route or endpoint?
An endpoint is a description of what action the client is able to perform
on a particular page of the app.
5. What is the difference between GET and POST?
A GET request is idempotent, meaning all get requests do not alter 
any of the data it is requesting from the database. A POST request
is a request that alters the data in some form.
5. How would you explain what RESTful routing is?
RESTful routing is the convention or standard to be followed when creating 
CRUD apps. RESTful routing is very specific in terms of what routes should
look like and how they function in terms of the resource.
6. What is SQL?
SQL is a database language that allows developers to create/edit and delete
database schema.
7. What is a relational database?
A relational databse is a databse that permits the relationship between
tables.
8. How would you explain what a redirect is?
A redirect is the action of runnning a view function and then sending the user to a particular page after some action is carried out by the client.
9. What is the difference between `redirect` and `render_template`? When would you use one or the other?
A redirect is always used after a POST request is submiitted and it involves running 
a particular view function and then sending the client to a partiuclar page. 
Render Template is used to send the client directly to a page without running a viewfunction.

- What does the following code do?

```py
student = Student('Joel', 'Burton')
db.session.add(student)
db.session.commit(student)
```
1)creating a new instance of the student class.
2)adding that new instance to the database by starting a transaction.
3) ending the transaction.
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
1) If a new student is added by the client, a POST request is sent to add that user
to the database and after the new student is created/added to the databse/and the transaction is complete, a redirect is run to run the same view function however,
now the request is a GET request so the view function returns a render template and 
sends the client directly to the "index.html" page and is passing the list of 
students as an argument so the html page can render all of the students on the page.

- What does the following code do?

```sh
flask db init
```
1) initiliazes migration on a particular project and allows versions of the database to be tracked. 

- What does the following code do?

```sh
flask db migrate -m "adding favorite_color column to students table"
```
Creates a version of the current database but does not add the tables yet. For this particular version, its file name will end with the mesage "adding favorite_color column to students table" so that the developer can easily track what versions are doing what.

- What does the following code do?

```sh
flask db upgrade
```
Commits the changes and adds the tables to the databse.

- Given the resource `students` - write out all 7 RESTful routes (include the HTTP verb and endpoint)

@app.route("/")
def root():
return redirect("index")

@app.route("/students", methods = ["GET", "POST"])
def index:
all_students = Student.query.all()
if request.method == b"POST":
    db.session.add(new_student)
    db.commit(student)
    return redirect("index")
return render_template("index.html", students = all_students)

@app.route("/students/new")
def new_student():
return render_template("students/new.html")

@app.route("/students/show", methods = ["GET", "PATCH"])
def show():
all_students = Student.query.all()
if request.method == b"PATCH":
    db.session.add(student)
    db.session.commit(student)
    all_students = Student.query.all()
    return redirect(url_for("index", students = all_students))
return render_template("index.html", students = all_students)

app.route("students/<int:id>/delete)




@app.route("students/<int:id>/edit")
def edit(id):
return render_template("edit.html", id = id)







"/students" GET
"/students/new" GET
"/students/" POST
"/students/show" GET
"/students/<int:id>/edit" GET
"/students/show" PATCH
"students/<int:id>/delete DELETE



- Imagine we want to add another resource for `excuses` which is a 1 to Many with `students` - write out all 7 RESTful routes that nest excuses inside of students (include the HTTP verb and endpoint)

"students/messages" GET
"students/<int:id>/messages" GET
"students/<int:id>/messages/new" GET
"students/<int:id>/messages POST
"students/<int:id>/messages/<int:message-id>/edit" GET
"students/<int:id>/messages/<int:message-id>/show" PATCH
"students/<int:id>/messages/<int:message-id>/delete" DELETE


