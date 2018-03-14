# Backend Conceptual Warmup

## Instructions

* Fork and clone this repository
* Place your answers inside of this file (you can keep these answers to a sentence or two)
* Submit a pull request to submit the assignment

## Questions

1.  What is Jinja2 used for?
    Jinja2 is for inserting backend code to our html templates.
2.  What is a migration? What is the purpose of a migration? Migration is like git but for databases. It is used to successfully update your database without dropping any of the data. It also gives you the ability to downgrade back to old versions of your database. Think of it as a Version Control Control System.
3.  What is a model? A Model is a class in which you tell your database the structure of your table (DDL). Columns, columns names, types, unique ids, relationships with other tables, tablename.
4.  What is a route or endpoint? A Route is a decoration that points to the location that the server should respond to a request with.
5.  What is the difference between GET and POST? GET is a request to a server that simply brings back data unchanged/modifues. You use a POST request to tell the server that you want modified data. Updated info, deleting info, creating info.
6.  How would you explain what RESTful routing is? It is a convention in the software community of naming your routes. /users, /users/new, users/<int:id>/show...
7.  What is SQL? SQL is the database language.
8.  What is a relational database? a relational database is one where there is a one to many association. the tables are usually all linked to the main table via an unique id.
9.  How would you explain what a redirect is?
10. What is the difference between `redirect` and `render_template`? When would you use one or the other? A redirect is directing the one function to another. Render_template communicates to the browser that we need to take our route to a new CRUD template that is stored in our templates folder. The function/server is responding with a new html page.

* What does the following code do? The following code creates an instance of the Student model, gives it the data and then starts the process of adding that data to our database(db,session.add) and places it in the database table with the commit. closing that request to add data.

```py
student = Student('Joel', 'Burton')
db.session.add(student)
db.session.commit(student)
```

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

* What does the following code do? this initializes the migration functionality between the server and database adding a migrations/versions folder. Now we can begin migrating and upgrading our table

```sh
flask db init
```

* What does the following code do? This is adding a migration (starting an upgrade to our database) to our versions file that we want to add a favorite_color column to our students table. It will not been actually added until we write the "flask db upgrade" command in our terminal.

```sh
flask db migrate -m "adding favorite_color column to students table"
```

* What does the following code do? This commits our migration to the database. If we were looking at our previous migration request above now we have a favorite_color column in our students table.

```sh
flask db upgrade
```

* Given the resource `students` - write out all 7 RESTful routes (include the HTTP verb and endpoint)
  VERB ENDPOINT
  GET "/" - root
  GET "/students"
  POST "/students"
  POST "/students/new"
  GET "/students/<int:id>
  GET "/students/<int:id>/edit"  
  POST "/students/<int:id>
  DELETE "/students/<int:id>

* Imagine we want to add another resource for `excuses` which is a 1 to Many with `students` - write out all 7 RESTful routes that nest excuses inside of students (include the HTTP verb and endpoint)
  GET "/students/<int:student_id>/excuses"
  POST "/students/<int:student_id>/excuses"
  POST "/students/<int:student_id>/excuses/new" -
  GET "/students/<int:student_id>/excuses/<int:id>"
  PATCH "/students/<int:student_id>/excuses/<int:id>
  GET "/students/<int:student_id>/excuses/<int:id>/edit"
  DELETE "/students/<int:student_id>/excuses/<int:id>
