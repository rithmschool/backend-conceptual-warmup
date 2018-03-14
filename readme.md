# Backend Conceptual Warmup

## Instructions

- Fork and clone this repository
- Place your answers inside of this file (you can keep these answers to a sentence or two)
- Submit a pull request to submit the assignment

## Questions

1. What is Jinja2 used for? 
Jinja is used to evaluate python script inside of html documents. 
2. What is a migration? What is the purpose of a migration?
A migration is a change in the DDL of an SQL database. A migration is used to consolidate changes into single steps which can be upgraded or downgraded, such as adding a column to a table. 
3. What is a model?
A model is an archetype for information to fit into. 
4. What is a route or endpoint?
A route/endpoint is the destination of a particular path or URL.
5. What is the difference between GET and POST?
GET is a request that simply retrieves information and does not change it, idempotent. A POST request is used when information needs to be modified or added to an existing database. 
5. How would you explain what RESTful routing is?
RESTful routing is a "model" or convention adopted by programmers to standardize the way that routes and paths are constructed when following CRUD (create, read, update, delete). The path, when widely adopted by programmers, makes it easy to assimilate new programmers or others into existing projects because the architecture of templates and routes remains similar for a larger variety of topics. 
6. What is SQL?
SQL is a programming language that works primarily with databases, communicating between databases, modifying them, retrieving information, etc. 
7. What is a relational database?
A relational database is essentially a table of data that also corresponds to another table, where "relationships" and information are tied to one another. For example, column 1 could be a person in one table, and another table could correspond to that person, but store entirely separate information such as favorite foods, rather than first and last name. This allows us to better organize information into smaller tables.
8. How would you explain what a redirect is?
A redirect is when your current request is processed and sent to another URL/endpoint/route. For example, a 404 page is a redirect from whatever invalid route you tried to access to a standard error page applied to invalid routes in general.
9. What is the difference between `redirect` and `render_template`? When would you use one or the other?
A render_template is to load a template page of HTML, whereas a redirect will return a programmed function, which then in turn will process whatever is written inside of it. They can both be used to guide the user to another destination.

- What does the following code do?

```py
student = Student('Joel', 'Burton')
db.session.add(student)
db.session.commit(student)
```

This creates a new instance of the class Student with the two properties "Joel" and "Burton" which I am assuming is first name and last name. Db session add opens a transaction with the SQL database that the class Student corresponds to, and halts all other information processing in that database until the session is finalized. The new instance of class Student that corresponds to Joel is then passed through to the database, and committed, finalizing the transfer of information.

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
When a user accesses the route *defaulturlhere*/students, the script will return the function index. The function has two methods GET and POST, meaning the user has the option to both read, but also update. If the request is a POST, the function creates a new instance of the class student with the first and last name Joel and Burton, then sends it to the database as mentioned above. After this is completed, the user is then redirected to the index function, which I would imagine displays all of the students and whatever other information is on the index page. If the request is a GET, the function will return the index.html document and pass through all of the students in the class student table to that file for jinja to process.


- What does the following code do?

```sh
flask db init
```

This initializes flask migrate so other operations can be performed. 

- What does the following code do?

```sh
flask db migrate -m "adding favorite_color column to students table"
```
This would attempt to create a migration with the message "adding favorite_color column to students table," and I assume that it would perform the task of adding a new favorite color column to the existing students table in SQL. 


- What does the following code do?

```sh
flask db upgrade
```
This finalizes the migration and lets flask migrate know that the transaction is done, I see it as similar to "git push" or "db.session.commit()" though I'm not sure technically if it's doing something else under the hood. 

- Given the resource `students` - write out all 7 RESTful routes (include the HTTP verb and endpoint)

@app.route("/")
def root():
    return redirect(url_for('index'))
    <!-- method is get by default / read-->


@app.route("/students", methods=['GET','POST'])
def index():
    return render_template('/students/index.html')

@app.route("/students/new")
def new():
    return redirect(url_for('index'))
    <!-- method is get by default / read-->

@app.route("/students/<int:id>/edit")
def edit():
    return render_template('/students/edit.html')
    <!-- method is get by default / read-->


@app.route("/students/<int:id>") 
def show():
    return render_template('/students/show.html')
    <!-- method is get by default / read -->

@app.route("/students/<int:id>/edit", method='PATCH')
def upgrade():
    return redirect(url_for('index'))


@app.route("/students/<int:id>", method='DELETE')
def destroy():
    return redirect(url_for('index'))

- Imagine we want to add another resource for `excuses` which is a 1 to Many with `students` - write out all 7 RESTful routes that nest excuses inside of students (include the HTTP verb and endpoint)


@app.route("/students/<int:id>/excuses")
def root_excuses():
    return redirect(url_for('index_excuses'))
        <!-- method is get by default / read --> 


@app.route("/students/<int:id>/excuses", methods=['GET','POST'])
def index_excuses():
    return render_template('/excuses/index.html')

@app.route("/students/<int:id>/excuses/new")
def new_excuses():
    return render_template('/excuses/new.html')
        <!-- method is get by default / read-->


@app.route("/students/<int:id>/excuses/<int:excuse_id>/edit")
def edit_excuses():
    return render_template('/excuses/edit.html')
        <!-- method is get by default / read-->


@app.route("/students/<int:id>/excuses/<int:excuse_id>")
def show_excuses():
    return render_template('/excuses/show.html')
        <!-- method is get by default / read-->


@app.route("/students/<int:id>/excuses/<int:excuse_id>/edit", method="PATCH")
def upgrade_excuses():
    return redirect(url_for('index_excuses'))


@app.route("/students/<int:id>/excuses/<int:excuse_id>/edit", method="DELETE")
def destroy_excuses():
    return redirect(url_for('index_excuses'))
<!-- 

I may have routed these differently than restful... I can't remember exactly if the methods are organized following the "restful" route but I think these are the main operations that need to be on a restful route.  



Yang 


-->