# Backend Conceptual Warmup

## Instructions

- Fork and clone this repository
- Place your answers inside of this file (you can keep these answers to a sentence or two)
- Submit a pull request to submit the assignment

## Questions

1. What is Jinja2 used for? 
#It is Python programing template language It is used to generate source code
2. What is a migration? What is the purpose of a migration?
# it is process of transfering data between computer storage files 
3. What is a model?
# it's place where you store sqlalchemy instance that you are creating.
4. What is a route or endpoint?
# Endpoint take some functions and return data to the client. 
5. What is the difference between GET and POST?
# Those are two different METHODS . There are used to transfer data from client to serever. Get usually has that url inside while post has like message body? 
5. How would you explain what RESTful routing is?
# It is routing resources for flask app.
6. What is SQL?
# It is structured Query Language to communicate with database
7. What is a relational database?
# Relational database is colectional data organized in tables that can be related to each other. 
8. How would you explain what a redirect is?
# Redirect  is what send client from one url to another? 
9. What is the difference between `redirect` and `render_template`? When would you use one or the other?
# redirect is where your url that you providwe will take you, render template is method that when you pass something you go there :/
- What does the following code do?

```py
student = Student('Joel', 'Burton')
db.session.add(student)
db.session.commit(student)
```

# Adding name of this students to the database.

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

# Adding name of this students to the database, and returning you back to index page

- What does the following code do?

```sh
flask db init

# It is first step ( out of three) in migrating some data into database.
```

- What does the following code do?

```sh
flask db migrate -m "adding favorite_color column to students table"

# it is second step in that process. It will triggered migration file in your fila that you working with that following message.
```

- What does the following code do?

```sh
flask db upgrade
```

# that third step in same process; finishing treansaction

- Given the resource `students` - write out all 7 RESTful routes (include the HTTP verb and endpoint)

/student   

/student/new   ( new)   GET

/student/edit   (edit)  GET

/student/show   (show)  GET

/student/delete

/student/add

/student/update?

- Imagine we want to add another resource for `excuses` which is a 1 to Many with `students` - write out all 7 RESTful routes that nest excuses inside of students (include the HTTP verb and endpoint)


don't really know this out of head. :(

/student/<id>/excuses   

/student/new/excuses  ( new)   GET

/student/edit/id>/excuses/<excuse_id   (edit)  GET

/students/<id>/excuses/<excuse_id  (show)  GET

/student/delete/<id>/excuses 

/student/add/<id>/excuses 

/student/update?/<id>/excuses 


