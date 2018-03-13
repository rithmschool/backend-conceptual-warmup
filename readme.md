# Backend Conceptual Warmup

## Instructions

- Fork and clone this repository
- Place your answers inside of this file (you can keep these answers to a sentence or two)
- Submit a pull request to submit the assignment

## Questions

1. What is Jinja2 used for?
2. What is a migration? What is the purpose of a migration?
3. What is a model?
4. What is a route or endpoint?
5. What is the difference between GET and POST?
5. How would you explain what RESTful routing is?
6. What is SQL?
7. What is a relational database?
8. How would you explain what a redirect is?
9. What is the difference between `redirect` and `render_template`? When would you use one or the other?

- What does the following code do?

```py
student = Student('Joel', 'Burton')
db.session.add(student)
db.session.commit(student)
```

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

- What does the following code do?

```sh
flask db init
```

- What does the following code do?

```sh
flask db migrate -m "adding favorite_color column to students table"
```

- What does the following code do?

```sh
flask db upgrade
```

- Given the resource `students` - write out all 7 RESTful routes (include the HTTP verb and endpoint)
